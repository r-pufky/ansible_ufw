# UFW
Uncomplicated Firewall configuration.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_ufw/blob/main/meta/main.yml)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_ufw/tree/main/defaults/main/)

## Dependencies
**galaxy-ng** roles cannot be used independently. Part of
[r_pufky.deb](https://github.com/r-pufky/ansible_collection_deb) collection.

## Example Playbook
Read through defaults before using. Simple and easy configuration of UFW with
multiple rules and hosts.

This will enable SSH with logging on all hosts. The example host will have SSH
enabled as well as an incoming port of 2222, outgoing port of 443, and deny any
additional outgoing connections.

group_vars/all/vars/main.yml
``` yaml
ufw_group:
  - proto: 'tcp'
    from_ip: 'any'
    to_port: 22
    direction: 'in'
    log: true
    comment: 'ssh'
```

host_vars/ufw.example.com/vars/ufw.yml
``` yaml
ufw_default_outgoing: 'deny'
ufw_host:
  - proto: 'tcp'
    from_ip: 'any'
    to_port: 2222
    direction: 'in'
    comment: 'allow incoming to port tcp/2222'
  - proto: 'tcp'
    to_ip: 'any'
    to_port: 443
    direction: 'out'
    comment: 'allow outgoing to port tcp/443'
  - proto: 'tcp'
    to_ip: 'any'
    to_port: 22
    direction: 'out'
    comment: 'allow outgoing ssh to port tcp/22'
```

Apply the role
``` yaml
- name: 'Manage UFW'
  hosts: '*'
  become: true
  roles:
     - 'r_pufky.deb.ufw'
```

## Development
Configure [environment](https://github.com/r-pufky/ansible_collection_docs/blob/main/dev/environment/README.md)

Run all unit tests:
``` bash
molecule test --all
```

### Releases
Major release versions track Debian release versions:

* **[13.x.x](https://github.com/r-pufky/ansible_ufw)**: 13 Trixie.
* **[12.x.x](https://github.com/r-pufky/ansible_ufw/tree/12.x)**: 12 Bookworm.

### Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_ufw/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
