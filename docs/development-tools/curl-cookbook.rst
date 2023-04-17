==================
Curl cookbook
==================

This guide collects curl spell founds over the internet and stack overflow.

Send a POST Request with Data from a File
*****************************************

This is a realistic curl spell POST a SOAP xml request to ws endpoint.

.. code-block:: bash

  $ curl --header "Content-Type: text/xml;charset=UTF-8" \
       --header "SOAPAction: \"MySoapAction\"" \
       --data @data.xml http://localhost:8080/ws/

where data looks like

.. code-block:: bash

    <?xml version="1.0" encoding="UTF-8"?>
    <soapenv:Envelope
        xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
        xmlns:xsd="http://www.w3.org/2001/XMLSchema"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <soapenv:Body>
            <GetEmployeeInfo>
                <EmployeeNumber>12345678</EmployeeNumber>
             </GetEmployeeInfo>
        </soapenv:Body>
    </soapenv:Envelope>


Similar spell but explicitly define HTTP method, and url

.. code-block:: console

    curl --request POST --data-binary @data.json --header 'Content-Type: application/vnd.api+json' --url http://localhost:3111/ws


Using curl to download a file
*****************************

.. code-block:: bash

    curl -OL https://dlcdn.apache.org/cassandra/3.11.13/apache-cassandra-3.11.13-bin.tar.gz

-L, --location Follow Location header if resource is moved.
-O, --remote-name Write  output to a local file named

Using curl to find Time to First Byte
**************************************

.. code-block:: bash

   $ curl -w "Connect time: %{time_connect} Time to first byte: %{time_starttransfer} Total time: %{time_total} \n" -o /dev/null www.google.fi
     % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
    100 14948    0 14948    0     0  43891      0 --:--:-- --:--:-- --:--:-- 44620
    Connect time: 0.036681 Time to first byte: 0.306465 Total time: 0.340567


Also you can create a file like ::

    $ cat curl-format.txt
    time_namelookup:  %{time_namelookup}s\n
            time_connect:  %{time_connect}s\n
         time_appconnect:  %{time_appconnect}s\n
        time_pretransfer:  %{time_pretransfer}s\n
           time_redirect:  %{time_redirect}s\n
      time_starttransfer:  %{time_starttransfer}s\n
                         ----------\n
              time_total:  %{time_total}s\n

And use like ::

  curl -w "@curl-format.txt" -o /dev/null www.google.fi
  time_connect:  0.027s
     time_appconnect:  0.000s
    time_pretransfer:  0.027s
       time_redirect:  0.000s
  time_starttransfer:  0.099s
                     ----------
          time_total:  0.102s


Interesting links
*****************

* `<https://catonmat.net/cookbooks/curl/make-post-request>`_
* `<https://blog.josephscott.org/2011/10/14/timing-details-with-curl/>`_

