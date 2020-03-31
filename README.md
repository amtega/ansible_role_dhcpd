# Ansible dhcpd role

This is an [Ansible](http://www.ansible.com) role to setup a dhcpd server.

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Example Playbook

This is an example playbook:

```yaml
---
- hosts: localhost  
  vars:
    dhcpd_subnets:
      - name: dhcp_subnet_0
        subnet: 192.168.13.0
        netmask: 255.255.255.0
        routers:
          - 192.168.13.1
        dns_servers:
         - 192.168.13.2
         - 192.168.13.3
        range_start: 192.168.13.100
        range_end: 192.168.13.120
        default_lease_time: 21600
        max_lease_time: 43200
        next_server: 192.168.13.13
        filename: pxelinux.0

      - name: dhcp_subnet_1
        subnet: 192.168.14.0
        netmask: 255.255.255.0
        routers:
          - 192.168.14.1
        dns_servers:
         - 192.168.14.2
         - 192.168.14.3
        range_start: 192.168.14.100
        range_end: 192.168.14.120
        default_lease_time: 21600
        max_lease_time: 43200
        next_server: 192.168.14.13
        filename: pxelinux.0

    dhcpd_hosts:
      - hostname: hostacme1
        mac: c5:6f:75:cc:00:01
        ipv4_address: 192.168.14.120

      - hostname: hostacme2
        mac: c5:6f:75:cc:00:02
        ipv4_address: 192.168.14.121
  roles:
    - amtega.dhcpd
```

## Testing

Tests are based on docker containers. You can setup docker engine quickly using the playbook `files/setup.yml` available in the role [amtega.docker_engine](https://galaxy.ansible.com/amtega/docker_engine).

Once you have docker, you can run the tests with the following commands:

```shell
$ cd amtega.dhcpd/tests
$ ansible-playbook main.yml
```

## License

Copyright (C) 2019 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Juan Antonio Valiño García.
- dhcp-lease-list script based on the one available in [isc-dhcp](https://sources.debian.org/src/isc-dhcp)
