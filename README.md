# Ansible dhcpd role

This is an [Ansible](http://www.ansible.com) role to setup a dhcpd server. This role is complemented with dhcpd_subnet and dhcpd_static to setup subnet and static addresses.

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
