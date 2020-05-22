# Ansible Role : firewall

Configures either ufw or firewalld depending on if the systems is based on Debian or RedHat.

## Requirements

None.

## Role Variables

### defaults/main.yml

### vars/RedHat.yml

    __firewall_package: firewalld

The name of the firewall package on RedHat based systems.  This value is used to define firewall_package_name in the tasks/main.yml file.  This value can be overridden by setting firewall_package_name in the playbook.

### vars/Debian.yml

    __firewall_package: ufw

The name of the firewall package on Debian based systems.  This value is used to define firewall_package_name in the tasks/main.yml file.  This value can be overridden by setting firewall_package_name in the playbook.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - glillico.firewall

## License

MIT

## Author Information

This role was created in 2020 by Graham Lillico.
