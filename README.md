# Ansible Role : configure_firewall

Installs and configures either ufw or firewalld depending on if the systems is based on Debian or RedHat.

## Requirements

None.

## Role Variables

### defaults/main.yml

#### ufw

|Variable|Description|
|---|---|
|firewall_ufw_rule|Add a firewall rule.<br>(Options: allow, deny, limit, reject), (Default: null).|
|firewall_ufw_direction|The direction for the rule.<br>(Options: in, incoming, out, outgoing, routed), (Default: null).|
|firewall_ufw_interface|The network interface for rule.|
|firewall_ufw_from_ip|The source IP address.|
|firewall_ufw_from_port|The source port|
|firewall_ufw_to_ip|The destination IP address.|
|firewall_ufw_to_port|The destination port.|
|firewall_ufw_proto|The TCP/IP protocol for the rule.<br>(Options: any, tcp, udp, ipv6, esp, ah, gre, igmp), (Default: null).|
|firewall_ufw_comment|A comment for the rule.|

#### firewalld

|Variable|Description|
|---|---|
|firewall_firewalld_state|Should the rule be enabled or disabled.<br>(Options: absent, disabled, enabled, present).|
|firewall_firewalld_port|The name or number of a port, can also be used to define a port range.<br>This should be in the format or *port/protocol* or *start_port-end_port/protocol* for port ranges.<br>(Default: null).|
|firewall_firewalld_zone|The firewalld zone to add/remove the rule to/from.|

### vars/RedHat.yml

|Variable|Description|
|---|---|
|__firewall_package: firewalld|The name of the firewall package on RedHat based systems.<br>This value is used to define firewall_package_name in the tasks/main.yml file.<br>This value can be overridden by setting firewall_package_name in the playbook.|

### vars/Debian.yml

|Variable|Description|
|---|---|
|__firewall_package: ufw|The name of the firewall package on Debian based systems.<br>This value is used to define firewall_package_name in the tasks/main.yml file.<br>This value can be overridden by setting firewall_package_name in the playbook.|

## Dependencies

None.

## Example Playbook

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - glillico.configure_firewall

## License

MIT

## Author Information

This role was created in 2020 by Graham Lillico.
