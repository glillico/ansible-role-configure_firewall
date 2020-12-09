# Ansible Role : configure_firewall

[![CI](https://github.com/glillico/ansible-role-configure_firewall/workflows/CI/badge.svg)](https://github.com/glillico/ansible-role-configure_firewall/actions?query=workflow%3ACI)

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

#### Examples
##### UFW Firewall

Limits the connections coming in on interfaec enp0s8 from 192.168.60.1 on TCP port 22.

```
  - firewall_ufw_rule: 'limit'
    firewall_ufw_direction: 'in'
    firewall_ufw_interface: 'enp0s8'
    firewall_ufw_from_ip: '192.168.60.1'
    firewall_ufw_from_port: ''
    firewall_ufw_to_ip: ''
    firewall_ufw_to_port: '22'
    firewall_ufw_proto: 'tcp'
    firewall_ufw_comment: ''
```

##### firewalld Firewall

Enable the public zone to accept TCP connections on port 8080.
```
  - firewall_firewalld_state: 'enabled'
    firewall_firewalld_port: '8080/tcp'
    firewall_firewalld_zone: 'public'
```

Disables the cockpit service on the public zone.
```
  - firewall_firewalld_state: 'disabled'
    firewall_firewalld_service: 'cockpit'
    firewall_firewalld_zone: 'public'
```

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

Created in 2020 by Graham Lillico.
