Role Name
=========

The te_agent role installs, configures, and manages the services of the
Tripwire Enterprise Agent.

Requirements
------------

The Tripwire Enterprise Agent needs a Tripwire Enterprise Console server
to connect to. The server hostname and services passphrase are needed
to configure the Agent.

The installer file for the Agent must also be available on the Ansible
control machine, for copying to the remote host for installation.

Role Variables
--------------

```yaml
# REQUIRED variables (no default defined)
#########################################

# Must be set to the path to the agent installer. Is copied to a
# temporary directory on the remote host for installation
te_agent_package_source: ~
# Must be set to the hostname or IP address of the Tripwire Enterprise console
te_agent_te_server_host: ~
# Must be set to the service passphrase for the Tripwire Enterprise console
te_agent_te_services_passphrase: ~

# OPTIONAL variables (no default)
#################################

# If set, used to determine if the package needs to be upgraded
te_agent_package_version: ~
# If set, is written to the agent tags file for initial registration
te_agent_tags: ~


# from defaults/main.yml
te_agent_package_state: present
te_agent_package_install_path: '/usr/local/tripwire/te/agent'
te_agent_te_services_port: 9898
te_agent_te_server_http_port: 8080
te_agent_local_port: 9898
te_agent_install_rtm: true
te_agent_proxy_port: 1080
te_agent_rtm_port: 1169
te_agent_enable_fips: false
te_agent_service_state: started
te_agent_service_enabled: true
# only makes sense if te_agent_install_rtm = true
te_agent_service_rtm_state: started
te_agent_service_rtm_enabled: true

# from vars/defaults.yml (should not be changed)
te_agent_package_name: te_agent
te_agent_service_name: twdaemon
te_agent_service_rtm_name: twrtmd

# from vars/Windows.yml (should not be changed)
te_agent_package_name: '{CBE84CA6-F8E9-4D79-B8CE-CF936013DA82}'
te_agent_service_name: teagent
te_agent_service_rtm_name: tesvc
```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: te_agent
      te_agent_package_source: /mnt/data/te_agent/linux/x86_64/te_agent.bin
      te_agent_te_server_host: tw-testcon.example.com
      te_agent_te_services_passphrase: correct horse battery staple
      te_agent_package_version: 8.5.6
      te_agent_tags:
        foo: bar
        tags2: [taga, tagb]
```

License
-------

Licensed under the Apache 2.0 license. See the LICENSE and NOTICE files for details.

Author Information
------------------

Copyright 2017 Tripwire, Inc.

https://www.tripwire.com/
