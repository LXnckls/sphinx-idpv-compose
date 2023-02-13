.. index:: STA, Identity Provider
   :name: idp

==============================
Prepare STA Identity Provider
==============================

Users connecting a virtual card to their client have to authenticate against an OIDC Identity Provider. For the demo we use **SafeNet Trusted Access (STA)**.


IDPV Management Groups
-----------------------

In the **STA Token Management** console **create the following groups** that will be used to assign the required IDPV management roles::
   
   IDPV_Admins
   IDPV_Users
   IDPV_OfflineEnabled
   IDPV_ProvAdmins

.. thumbnail:: _images/STA-Add_Groups.png
   :width: 100%

.. note:: Make sure that any users that should later use IDPrime Virtual are part of the ``IDPV_Users`` group!



Create IDPV Application
------------------------

Create a new application in the **STA Access Management console** under "Applications". Therefore you have to search for the application **SafeNet IDPrime Virtual** and press the "+" button:

.. thumbnail:: _images/STA-Add_IDPV_App.png

From the **Step 01: SafeNet IDPrime Virtual Setup** section note the following 
   
 * ``Client ID``
 * ``Client Secret``
 * ``Well Known Configuration URL``

.. thumbnail:: _images/STA-IDPV-Step-1.png

Under **Step 02: STA Setup** set the following parameters:

 * Leave the **Service Login URL** empty
 * As **Valid Redirect URL** set ``https://<dns-hostname>/*``

.. thumbnail:: _images/STA-IDPV-Step-2.png

Finally on the **Assign Tab** map the application to the relevant user groups:

.. thumbnail:: _images/STA-IDPV_Assign_Users.png



Get further OIDC Parameters
----------------------------

To connect to this new application from the IDPV Server you have to collect further parameters. An easy way to read this data is to use `JSON formatter <https://jsonformatter.org>`_:

  * Click on **Upload Data** and copy and paste the **Well Known Configuration URL** noted before
  * Note the ``issuer`` and ``jwks_uri``

.. thumbnail:: _images/STA-JSON_formatter.png

Also open the ``jwks_uri`` in the `JSON formatter <https://jsonformatter.org>`_ and note the following entries:

  * ``kid``
  * ``e``
  * ``n``
