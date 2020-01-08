# RGM Metricbeat deploy ansible role

Ansible role to deploy metricbeat monitoring agent from RGM oneliner.

It perform following tasks :

- Install needed packages to perform metricbeat agent installation (lsb_release)
- Deploy metricbeat agent with RGM oneliner script
- Create new hosts into Lilac configuration
- Perform export job to include hosts in nagios

## Requirements

Some of this variables **absolutely need to be defined** to get fully working playbook :

- rgm_adm_username
- rgm_adm_password

## Role Variables

| name                             | default value             | usage                                                |
| -------------------------------- | --------------------------| ---------------------------------------------------- |
| ```rgm_ip```                     |                           | RGM IP or hostname to get install script and use API |
| ```d_rgm_template```             | RGM_LINUX_ES              | RGM template applied to new hosts                    |
| ```d_rgm_exportjob_name```       | Incremental Nagios Export | RGM export job name used to import new hosts         |
| ```d_rgm_win_template```         | RGM_WINDOWS_ES            | RGM template applied to new windows hosts            |
| ```rgm_adm_username```           |                           | RGM admin username to create new hosts               |
| ```rgm_adm_password```           |                           | RGM admin password to create new hosts               |
| ```remove_metricbeat_services``` | no                        | Launch only metricbeat service deletion              |

## Recommendations

To improve security usage of this role, we recommend to store all sensitives datas in ansible custom vault.  
All variables such as :

- `rgm_adm_username`
- `rgm_adm_password`
- `ansible_user` (for windows hosts)
- `ansible_password` (for windows hosts)
- `ansible_connection` (for windows hosts)
- `ansible_winrm_transport` (for windows hosts)
- `ansible_wirm_scheme` (for windows hosts)
- `ansible_port` (for windows hosts)

Note: You could store more other variables in vault such as `d_rgm_template` or `d_rgm_ip` to centralize variables filling.

## Dependencies

No specific dependencies expected here.

## Example Playbook

```yaml
---
- hosts: monitored
  roles:
    - role-metricbeat-deploy
  vars:
    rgm_ip: <rgm_hostname>
    rgm_adm_username: <rgm_admin_username>
    rgm_adm_password: <rgm_admin_password>
```

## License

BSD

## Author Information

Initial write by Vincent Fricou <vincent@fricouv.eu> (2019), release under the terms of BSD licences

### Contributions

Oriane SAVIO - Windows deployment parts