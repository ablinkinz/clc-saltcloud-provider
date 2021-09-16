#clc-saltcloud-provider
===================
salt-cloud provider for Century Link Cloud
===================
CenturyLink Cloud Module
===================

.. versionadded:: (DEVELOP BRANCH 2017.7+)

The CLC cloud module allows you to manage CLC Via the CLC SDK.

:codeauthor: Stephan Looney <slooney@stephanlooney.com> 


Dependencies
============

- clc-sdk Python Module

CLC SDK
-------

clc-sdk can be installed via pip:

.. code-block:: bash

    pip install clc-sdk

.. note::
  For sdk reference see: https://github.com/CenturyLinkCloud/clc-python-sdk

Configuration
=============

To use this module, set up the clc-sdk, username,password,key in the
cloud configuration at
``/etc/salt/cloud.providers`` or ``/etc/salt/cloud.providers.d/clc.providers.conf``:
.. code-block:: yaml

    clc:
      driver: clc
      user: 'web-user'
      password: 'verybadpass'
      token: ''
      token_pass:''

.. note::

    The ``provider`` parameter in cloud provider configuration was renamed to ``driver``.
    This change was made to avoid confusion with the ``provider`` parameter that is
    used in cloud profile configuration. Cloud provider configuration now uses ``driver``
    to refer to the salt-cloud driver that provides the underlying functionality to
    connect to a cloud provider, while cloud profile configuration continues to use
    ``provider`` to refer to the cloud provider configuration that you define.

'''
.. code-block:: yaml
Example cloud profile for CLC (linux)
``/etc/salt/cloud.profiles`` or ``/etc/salt/cloud.profiles/clc.profiles.conf``:
small_linux_instance:
    provider: 'clc'
    ssh_username: root
    ssh_password: "Admin2452"
    location: "VA1"
    template: "UBUNTU-14-64-TEMPLATE"
    cpu: "2"
    ram: "8"
    backup_level: "Standard"
    group: "SaltStack"
    description: "salt-cloud"
    network: "vlan_2848_10.127.248"
    password: "Admin2452"
    minion:
        master: 10.127.248.41
Examples (non traditional salt-cloud operations)
=============
To get an estimate of your monthly cloud costs:
salt-cloud -f get_monthly_estimate clc

To get your month to date cloud costs:
salt-cloud -f get_month_to_date clc group=<server group> location=<CLC datacenter name>

To get an estimate of your monthly cloud costs for a given group:
salt-cloud -f get_group_estimate clc 

To list all systems in your account
salt-cloud -f get_nodes_full clc

Query CLC for a list of alerts for a given server
salt-cloud -f get_server_alerts clc servername=<server to check up on>

