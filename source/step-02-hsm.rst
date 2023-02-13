.. index:: HSM
   :name: hsm

====================
Prepare HSM
====================

IDPV supports different types of HSM. For this eval installation you can find two different options below.


.. index:: SoftHSM

SoftHSM
--------

IDPV Server is pre-configured with **SoftHSM**, an emulation of a Hardware Security Module so you don't have to change any settings to use it.

.. note:: SoftHSM is intended for **pure demo environments only** and to avoid setting up a dedicated HSM service like a Luna appliance or DPoD!
   
   Also be aware that the content of the **SoftHSM only exists as long as the Container is not removed** as the HSM data exists only within the running instance!

You can check the SoftHSM credentials from within the container in the following file::

   $ cat SoftHsmDetails.txt


.. index:: DPoD
   :name: dpod

DPoD Luna Cloud HSM
--------------------

The Thales **Luna Cloud HSM** hosted on **Data Protection on Demand (DPoD)** offers a more secure option to encrypt the IDPV virtual smart cards. It should be used for evaluation setups and small production installations.

Download and unpack **DPoD Client** into a folder called ``dpod`` below your Docker project root (``idpv-eval`` in our example):

.. tabs::

   .. tab:: Windows

      .. highlight:: pwsh-session

      ::

         > Expand-Archive setup-dpod.zip

      ::

         > Expand-Archive cvclient-min.zip

      **Deploy DPoD configuration files** to your IDPV Server configuration folder::

         > Copy-Item Chrystoki.conf partition-ca-certificate.pem partition-certificate.pem server-certificate.pem ..\idpv\hsm\

      Test and configure DPoD Client from within folder ``dpod``::

         > .\setenv.cmd

      ::

         > .\lunacm.exe


   .. tab:: Linux

      .. highlight:: shell-session

      ::

         $ unzip setup-dpod.zip

      ::

         $ tar xf cvclient-min.tar

      **Deploy DPoD configuration files** to your IDPV Server configuration folder::

         $ cp Chrystoki.conf partition-ca-certificate.pem partition-certificate.pem server-certificate.pem ../idpv/hsm/

      Test and configure DPoD Client from within folder ``dpod``::

         $ source ./setenv

      ::

         $ bin/64/lunacm


.. note:: Executing the ``setenv`` script modifies ``Chrystoki.conf``, so it will be different from the original file copied previously!


**Initilize the partition** from the LunaCM command line::

   $ partition init -label IDPrimeVirtual

Initialize the **Crypto Officer** role::

   $ role login -name po

::

   $ role init -name co

::

   $ role logout

You have to **change the initial password** for the Crypto Officer role before it can be used::

   $ role login -name co

::

   $ role changepw -name co

::

   $ role logout
