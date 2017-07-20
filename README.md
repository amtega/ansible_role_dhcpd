# Ansible dhcpd role

This is an [Ansible](http://www.ansible.com) role to setup a dhcpd server.

## Requirements

- Ansible >= 2.3

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Dependencies

None.

## Example Playbook

This is an example playbook:

```yaml
---
- name: dhcpd sample
  hosts: localhost
  vars:
    dhcpd_subnets:
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
    - dhcpd
```

## Testing

Test are based on docker containers. You can run the tests with the following commands:

```shell
$ cd dhcpd/test
$ ansible-playbook main.yml
```

If you have docker engine configured you can avoid running dependant 'docker_engine' role (that usually requries root privileges) with the following commands:

```shell
$ cd dhcpd/test
$ ansible-playbook --skip-tags "role::docker_engine" main.yml
```

## License

Not defined.

## Author Information

- Juan Antonio Valiño García ([juanval@edu.xunta.es](mailto:juanval@edu.xunta.es)). Amtega - Xunta de Galicia
