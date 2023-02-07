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

Interesting links
*****************

* `<https://catonmat.net/cookbooks/curl/make-post-request>`_
