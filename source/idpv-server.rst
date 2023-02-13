.. index:: IDPV Server
   :name: idpv-server

====================
Install IDPV Server
====================

The following sections describe a standard evaluation setup for IDPV.



Setup IDPV Server
------------------

The following folders should exist below your Docker project root directory (``idpv-eval`` in this documentation):

* ``dpod`` - Only required if :ref:`Luna Cloud HSM <dpod>` is used
* ``idpv`` - IDPV Server image and config templates

  * ``config`` - IDPV configuration files to be mapped into Docker Container
  * ``hsm`` - Luna HSM configuration files to be mapped into Docker Container



Configure IDPV Server
----------------------

The IDPV Server software archive contains a folder with the configuration file templates. Copy the following files to ``idpv/config`` and edit them according to the parameters collected during the ":ref:`idpv-preparation-steps`":

* ``appsettings.yml`` - IDPV settings related to database, HSM/DPoD, and server interface
* ``idp-configuration.json`` - OIDC communication and policy settings
* ``log4net.config`` - Logging settings
* ``policy-configuration.json`` - IDPV policy settings for the virtual cards

There are further details concerning the configuration options that are described in section :ref:`appendix-idpv-config` in the appendix.



Import IDPV Docker Image
-------------------------

.. highlight:: shell-session

Import IDPV Server Docker image::

   $ docker load -i idprimevirtual_server_evaluation.tar.gz

You can check the imported image name and version tag using the following command::

   $ docker image ls

To easily address the image you can add an additional tag to the imported image::

   $ docker image tag idprimevirtual_server_evaluation:<version> idpv:latest

Now you can address the image using the tag ``idpv:latest`` as it is configured in the :download:`compose.yaml <_static/compose.yaml>` file.



Run IDPV Server
----------------

To run the IDPV Server instance in detached mode you can simply run your Docker Compose environment::

   $ docker compose up -d

Follow the last 25 lines of the log, which should display the important output if the server is successfull up and running::

	$ docker logs -n 25 -f idpv



Create IDPV Tenant
-------------------

Now you can create your first tenant by opening a "bash" in the Docker container::

   $ docker exec -it idpv bash

You have to execute the ``SetupTenant create`` command in the Docker Container which requires the following parameters:

* ``-i`` - Define the ``idp-configuration.json`` with the IDP communication settings
* ``-p`` - Set the virtual card policy using the ``policy-configuration.json`` file
* ``-a`` - Set the IDP Client Secret
* ``-n`` - Create a "Tenant Name" to easily identify the tenant
* ``-k`` - Key export flag to prevent offline storage of private keys

::

   $ setuptenant/Thales.IDPrimeVirtual.SetupTenant create -i /publish/Config/idp-configuration.json -p /publish/Config/policy-configuration.json -k true -n Eval -a <idp_client_secret>



Update IDPV Tenant Configuration
---------------------------------

Whenever you want to change any tenant setting related to the **IDP configuration** or the **virtual card policy** you need to call the ``SetupTenant update`` command::

   $ setuptenant/Thales.IDPrimeVirtual.SetupTenant update -t <tenant_id>



.. index:: Troubleshooting; Server

Troubleshooting
----------------

To troubleshoot the server you can check the following places.

**Swagger API connectivity**

   To check the connectivity between the client and the server you can open a browser to access the IDPV Server Swagger interface.

**IDPV Server Logs**

   To review the server status you can follow last 30 lines of IDPV Server logs::

      > docker logs -f -n 30 idpv

   