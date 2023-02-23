.. index:: IDPV Client
   :name: idpv-client

====================
Install IDPV Client
====================


Setup IDPV Client
--------------------

To setup the client components on Windows 10/11 you have to install:

* **SafeNet Authentication Client (SAC)**

  Choose the **Minidriver Profile** unless you have specific other requirements

* **[Alternatively] SafeNet Minidriver**

  It provides the necessary middleware libraries but only provides a minimal user interface compared to SAC

* **IDPrime Virtual Client**

  Install the client that is part of the IDPV software package. You need the following **configuration parameters** for the installation:

    * IDPrime Virtual Server URL
    * Tenant ID
    * Optional: Proxy



Client Configuration
---------------------

The IDPV Client config is stored in the **Windows Registry**::

   HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Thales\SafeNet IDPrime Virtual

.. note:: If you change the **IDPV tenant** entry in the Registry you have to exit the IDPV Client tool, restart the service "SafeNet IDPrime Virtual" and start IDPV Client again.



.. index:: Troubleshooting; Client

Troubleshooting
----------------

**IDPV Client Logs**

   IDPV Client logs all error messages into the **Windows EventLog**.
   

**SAC Debug Logs**

To get further debug informationen you can activate the **SAC Logs** in the **SAC Client GUI**:

   * Open the "Advanced View" in the SAC GUI
   * Click on "Client Settings" and choose the "Advanced" tab
   * Click on the "Enable Logging" button

   .. thumbnail:: _images/SAC-Enable_Logging.png

   The **trace files** can then be found in the folder ``C:\Windows\Temp\eToken.log``. To review these files you need to install the **SAC LogViewer** from the SAC SDK software package.

   Alternatively the debug logs can also be configured be setting the following **Registry Key**:: 

      HKEY_LOCAL_MACHINE\SOFTWARE\SafeNet\Authentication\SAC\Log

   There you have to define the following values::

      "Enabled"=dword:00000001
      "maxfilesize"=dword:0c800000
      "days"=dword:0000016d
