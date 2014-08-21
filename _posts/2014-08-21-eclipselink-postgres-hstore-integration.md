---
layout: post
title: Eclipselink Postgres hstore type Integration
---

This [article](http://blog.interlinked.org/tutorials/postgresql.html) is a perfect introduction to about [postgres hstore type](http://www.postgresql.org/docs/9.0/static/hstore.html)
Available in postgres from version 9.2 through hstore extension. But how to use this type using JDBC or through eclipselink is not that popular.
In this article I will describe my personal approach.

## Download the PGHStore.java
By the time of writing this the utility: [PGHStore](http://archives.postgresql.org/pgsql-jdbc/2009-12/msg00037.php) is not included in the current jdbc-postgres-driver.

So get the file from the previous link. This is just an extract [PGHStore.java](https://github.com/antoniomaria/gazpachoquest/blob/master/persistence/jpa/src/main/java/net/sf/gazpachoquest/jpa/converter/support/PGHStore.java):

```java
package net.sf.gazpachoquest.jpa.converter.support;

import org.postgresql.util.PGobject;

/**
 * This implements a class that handles the PostgreSQL contrib/hstore type
 */
public class PGHStore extends PGobject implements Serializable, Cloneable, Map<String, String> {
    private final static long serialVersionUID = 1;
    private Map<String, String> _map;

    /**
     * required by the driver
     */
    public PGHStore() {
        setType("hstore");
        _map = new HashMap<String, String>();
    }
...

}
```

## HstoreSupport
This is a simple utility class which converts Map<String,String> into a String using the postgres hstore syntax.
This is just an extract of the [HstoreSupport.java](https://github.com/antoniomaria/gazpachoquest/blob/master/persistence/jpa/src/main/java/net/sf/gazpachoquest/jpa/converter/support/HstoreSupport.java)
Copied originally from [here](https://github.com/phstudy/jpa-converter-sample/blob/master/src/main/java/net/backtothefront/HstoreHelper.java)

```java

public class HstoreSupport {

    private static final String K_V_SEPARATOR = "=>";

    public static String toString(Map<String, String> m) {
        if (m.isEmpty()) {
            return "";
        }
        StringBuilder sb = new StringBuilder();
        int n = m.size();
        for (String key : m.keySet()) {
            sb.append(key + K_V_SEPARATOR + m.get(key));
            if (n > 1) {
                sb.append(", ");
                n--;
            }
        }
        return sb.toString();
    }

    public static Map<String, String> toMap(String s) {
        Map<String, String> m = new HashMap<String, String>();
        if (StringUtils.isBlank(s)) {
            return m;
        }
        String[] tokens = s.split(", ");
        for (String token : tokens) {
            String[] kv = token.split(K_V_SEPARATOR);
            String k = kv[0];
            k = k.trim().substring(1, k.length() - 2);
            String v = kv[1];
            v = v.trim().substring(1, v.length() - 2);
            m.put(k, v);
        }
        return m;
    }
}
```

## Creating the Eclipse link Hstore converter

Putting all the piece together, we get the [MapToStringConverter.java]([PGHStore.java](https://github.com/antoniomaria/gazpachoquest/blob/master/persistence/jpa/src/main/java/net/sf/gazpachoquest/jpa/converter/MapToStringConverter.java).
This is just an extract:

```java

import net.sf.gazpachoquest.jpa.converter.support.HstoreSupport;
import org.eclipse.persistence.mappings.converters.Converter;

public class MapToStringConverter implements Converter {

    private static final long serialVersionUID = 7555313947774805921L;

    @SuppressWarnings("unchecked")
    @Override
    public Object convertObjectValueToDataValue(Object objectValue, Session session) {
        Validate.isInstanceOf(Map.class, objectValue);
        Map<String, String> map = (Map<String, String>) objectValue;
        if (map.isEmpty()) {
            return null;
        }
        Object dataValue = null;

        if (isPostgresProvider(session)) {
            dataValue = new PGHStore(map);
        } else {
            dataValue = HstoreSupport.toString(map);
        }
        return dataValue;
    }

    @Override
    public Object convertDataValueToObjectValue(Object dataValue, Session session) {
        Object objectValue = null;
        if (dataValue == null) {
            return new HashMap<>();
        }
        if (dataValue instanceof Map) {
            objectValue = dataValue;
        } else if (dataValue instanceof String) {
            objectValue = HstoreSupport.toMap((String) objectValue);
        } else {
            throw new IllegalStateException(dataValue + " is not a valid map representation");
        }
        return objectValue;
    }

    @Override
    public boolean isMutable() {
        return false;
    }

    @Override
    public void initialize(DatabaseMapping mapping, Session session) {
        if (isPostgresProvider(session)) {
            mapping.getField().setSqlType(java.sql.Types.OTHER);
        } else {
            mapping.getField().setSqlType(java.sql.Types.VARCHAR);
        }
    }
}
```

## Use the converter in your JPA entities

This is an [example](https://github.com/antoniomaria/gazpachoquest/blob/master/persistence/domain/src/main/java/net/sf/gazpachoquest/domain/user/User.java):


```java
@Entity
@Table(name = "users")
public class User extends AbstractAuditable {

    @Column(unique = true)
    private String username;

    @Column
    private String password;

    @Column(nullable = false)
    private String givenNames;

    @Column(nullable = false)
    private String surname;

    @Column(nullable = false)
    private String email;

    @Column(name = "attributes")
    @Converter(name = "map-to-string-converter", converterClass = MapToStringConverter.class)
    @org.eclipse.persistence.annotations.Convert(value = "map-to-string-converter")
    private Map<String, String> attributes = new HashMap<String, String>();


```

