.. index:: IDPV; Preparation Steps
   :name: idpv-preparation-steps

========================
Preparation Steps
========================

The following steps describe the preparation required for an IDPV evaluation setup based on a **standardized Docker Compose configuration** to allow as much automation as possible.

.. toctree::
   :maxdepth: 1
   :hidden:
   :caption: Eval Installation Steps

   step-01-docker.rst
   step-02-hsm.rst
   step-03-idp.rst
   step-04-db.rst
   step-05-cert.rst
   

**Step 1: Setup Docker Compose**

   IDPV Server is based on a Docker image so for the evaluation setup we need a Docker Compose environment.


**Step 2: Prepare HSM**

   You have to prepare a **Hardware Security Module (HSM)**. In this evaluation setup we describe the usage of the build in **SoftHSM** as well as **Luna Cloud HSM from Data Protection on Demand (DPoD)**.

   .. hint:: You need to note the following parameters required later:

      * HSM Provider: ``SoftHSM``
      * Token Serial: ``3a2c9e2f0c303edc`` 
      * Token PIN: ``temp123#``


**Step 3: Prepare OIDC Identity Provider**

   You have to prepare an **OIDC Identity Provider**. In our case we use **SafeNet Trusted Access (STA)** but in general you can use any IDP supporting OpenID Connect (OIDC).

   .. hint:: You need to note the following parameters required later:

      * Client ID
      * Client Secret
      * Issuer URL
      * Redirect URL
      * Key ID ``kid``
      * Key Modulus ``n``
      * Key Exponent ``e``


**Step 4: Prepare Data Base**

   IDPV Server configuration is stored in a data base. For the evaluation setup we use a Docker image of **MySQL**.

   .. hint:: You need to note the following parameters required later:

      * DB Server: ``mysql``
      * Data Base: ``IDPrimeVirtualServer``
      * Username: ``idpvuser``
      * Password: ``mysqluser4idpv``


**Step 5: Create Server Certificate**

   IDPV enforces HTTPS between Client and Server. Therefore you have to create a Web Server Certificate.

   .. hint:: You need to note the folowing paramaters required later:

      * Certificate File: ``idpv.pfx``
      * Password: ``cert4idpv``
      * Fingerprint
