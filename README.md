# Ansible dhcpd role

This is an [Ansible](http://www.ansible.com) role to setup a dhcpd server that allows other hosts to add some configs to it.

## Requirements

- Ansible >= 2.4

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

By default the role assumes that you want to setup a full dhcpd server, but if the `dhcpd_server` points to another host the role works as a dhcpd client that allows you to setup parameters on a remote dhcpd server, and therefore it will skip all stuff related to dhcpd package install and daemon config.

## Dependencies

None.

## Example Playbook

This is an example playbook:

```yaml
---
- name: dhcpd sample
  hosts: localhost  
  vars:
    dhcpd_subnet_addresses:
      - subnet: "192.168.13.0"
        netmask: "255.255.255.0"
        routers: "192.168.13.1"
        dns_servers:
         - 192.168.13.2
         - 192.168.13.3
        range_start: 192.168.13.100
        range_end: 192.168.13.120
        default_lease_time: 21600
        max_lease_time: 43200
        next_server: 192.168.13.13
        filename: "pxelinux.0"

      - subnet: "192.168.14.0"
        netmask: "255.255.255.0"
        routers: "192.168.14.1"
        dns_servers:
         - 192.168.14.2
         - 192.168.14.3
        range_start: 192.168.14.100
        range_end: 192.168.14.120
        default_lease_time: 21600
        max_lease_time: 43200
        next_server: 192.168.14.13
        filename: "pxelinux.0"

    dhcpd_static_addresses:
      - hostname: hostacme1
        mac: c5:6f:75:cc:00:01
        ipv4_address: 192.168.15.120

      - hostname: hostacme2
        mac: c5:6f:75:cc:00:02
        ipv4_address: 192.168.15.121
  roles:
    - amtega.dhcpd
```

## Testing

Test are based on docker containers. You can run the tests with the following commands:

```shell
$ cd amtega.dhcpd/tests
$ ansible-playbook main.yml
```

If you have docker engine configured you can avoid running dependant 'docker_engine' role (that usually requries root privileges) with the following commands:

```shell
$ cd amtega.dhcpd/tests
$ ansible-playbook --skip-tags "role::docker_engine" main.yml
```

## License

Copyright (C) 2017 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify
it under the terms of:
GNU General Public License version 3, or (at your option) any later version;
or the European Union Public License, either Version 1.2 or – as soon
they will be approved by the European Commission ­subsequent versions of
the EUPL;

This role is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Juan Antonio Valiño García.
