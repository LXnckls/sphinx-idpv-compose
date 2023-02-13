.. index:: Certificate
   :name: cert

==========================
Create Server Certificate
==========================

IDPV enforces TLS encryption between server and client so you have to provide a web server certificate for your environment. For the eval setup we create a self-signed certificate with the following parameters:

* Folder ``idpv/config``
* Server Hostname: ``idpv``
* File: ``idpv.pfx``
* Password: ``cert4idpv``

Execute the following commands to **create a Certificate Signing Request (CSR)**, e.g. with server name "idpv"::

    $ openssl req -x509 -newkey rsa:2048 -nodes -keyout idpv.key -out idpv.csr -sha256 -days 365 -subj '/CN=idpv' -addext 'subjectAltName=DNS:idpv'

You can **check the CSR**::

    $ openssl x509 -in idpv.csr -text -noout

Create a **self-signed PKCS#12** certificate::

    $ openssl pkcs12 -export -out idpv.pfx -inkey idpv.key -in idpv.csr

Get the **fingerprint** of the certificate::

    $ openssl x509 -in idpv.csr -noout -fingerprint

