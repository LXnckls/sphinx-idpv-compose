.. index:: IDPV
   :name: idpv

===========================
IDPrime Virtual Eval Setup
===========================

This is a modified version of the `IDPrime Virtual Evaluation Setup Guide <https://safenet.readthedocs.io/projects/idpv>`_.

.. toctree::
   :maxdepth: 1
   :hidden:
   :caption: IDPV Eval Setup

   preparationSteps.rst
   idpv-server.rst
   idpv-client.rst
   appendix.rst


Solution Overview
------------------

`IDPrime Virtual (IDPV)`_ is a virtual smart card solution from `Thales DIS CPL`_. For the evaluation setup the following components are used:


* **Docker Environment**

  * `IDPrime Virtual Server`_ (Docker image from Support Portal)
  * `MariaDB`_ (Docker image)

* **OpenID Connect (OIDC) Identity Provider**

  * `SafeNet Trusted Access (STA)`_

* **Hardware Security Module (HSM)**

  * SoftHSM
  * `Luna Cloud HSM`_ on Thales Data Protection on Demand (DPoD)

* **Windows Client Components**

   * `SafeNet Authentication Client (SAC)`_ (Support Portal Download)
   * IDPrime Virtual Client


:ref:`genindex`
---------------

.. _`IDPrime Virtual (IDPV)`: https://cpl.thalesgroup.com/de/access-management/authenticators/pki-smart-cards/safenet-idprime-virtual
.. _`Thales DIS CPL`: https://cpl.thalesgroup.com>
.. _`IDPrime Virtual Server`: https://supportportal.thalesgroup.com/csm?id=csm_product&sys_id=16e029a94f0c3b48102400818110c725&table=sn_customerservice_product_name
.. _`MariaDB`: https://hub.docker.com/_/mariadb
.. _`SafeNet Trusted Access (STA)`: https://cpl.thalesgroup.com/access-management/safenet-trusted-access
.. _`Luna Cloud HSM`: https://cpl.thalesgroup.com/encryption/data-protection-on-demand/services/luna-cloud-hsm-services
.. _`SafeNet Authentication Client (SAC)`: https://supportportal.thalesgroup.com/csm?id=csm_product&sys_id=88303b92db852e00d298728dae96198e&table=sn_customerservice_product_name