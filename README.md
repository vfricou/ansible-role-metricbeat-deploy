# RGM Metricbeat deploy ansible role
## Job variables


### Mandatory extra-vars





Role Name
=========

Ansible role to deploy metricbeat monitoring agent from RGM oneliner.

It perform following tasks :
- Install needed packages to perform metricbeat agent installation (lsb_release)
- Deploy metricbeat agent with RGM oneliner script
- Create new hosts into Lilac configuration
- Perform export job to include hosts in nagios

Requirements
------------

Some of this variables **absolutely need to be defined** to get fully working playbook :

- d_rgm_ip
- rgm_adm_username
- rgm_adm_password

Role Variables
--------------

| name                       | default value             | usage                                                |
| -------------------------- | --------------------------| ---------------------------------------------------- |
| ```d_rgm_ip```             | 192.168.0.254             | RGM IP or hostname to get install script and use API |
| ```d_rgm_template```       | RGM_LINUX_ES              | RGM template applyed to new hosts                    |
| ```d_rgm_exportjob_name``` | Incremental Nagios Export | RGM export job name used to import new hosts         |
| ```rgm_adm_username```     |                           | RGM admin username to create new hosts               |
| ```rgm_adm_password```     |                           | RGM admin password to create new hosts               |

Dependencies
------------

No specific dependencies expected here.

Example Playbook
----------------

```yaml
---
- hosts: monitored
  roles:
    - role-metricbeat-deploy
  vars:
    d_rgm_ip: 192.168.0.10
    rgm_username: admin
    rgm_password: Chang€m€
```

License
-------

BSD

Author Information
------------------

Initial write by Vincent Fricou <vincent@fricouv.eu> (2019), release under the terms of BSD licences