# UFW
Uncomplicated Firewall configuration.

## [Requirements][i]
Requires [r_pufky.deb][g] galaxy-ng collection.

## Role Variables
Detailed variable use documented in defaults. See usage for role operation.

* [defaults][j] - User configurable options.

* [ufw_group][k] - UFW group configurable options.

* [ufw_host][l] - UFW host configurable options.

## Usage
Manage UFW with a single role application.

### Example Playbooks

This will enable SSH with logging on all hosts. The example host will have SSH
enabled for all hosts as well as an incoming port of 2222, outgoing port of
443, and deny any additional outgoing connections.

group_vars/all/vars/main.yml
``` yaml
ufw_cfg_group:
  - proto: 'tcp'
    from_ip: 'any'
    to_port: 22
    direction: 'in'
    log: true
    comment: 'ssh'
```

host_vars/ufw.example.com/vars/ufw.yml
``` yaml
ufw_srv_default_outgoing: 'deny'
ufw_cfg_host:
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

``` yaml
- name: 'Manage UFW'
  hosts: 'all'
  become: true
  roles:
     - 'r_pufky.deb.ufw'
```

## Development
Configure [environment][a].

``` bash
# Run all tests.
molecule test --all
```

### [Releases][b]

  Release | Debian | Ansible | Notes
 ---------|--------|---------|-------
  3.x.x   | 13     | 2.20    | Ansible 2.20, semantic versioning.
  2.x.x   | 13     | 2.18    | Migrate to Debian Trixie.
  1.x.x   | 12     | 2.18    | Use standardized libraries.
  0.x.x   | 12     | 2.11    | Migration from private repository.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License][c] | [direct link][f]

## Author Information
PGP: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9][d] | [github gist][e]


[a]: https://r-pufky.github.io/ansible_docs
[b]: https://semver.org/spec/v2.0.0
[c]: https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0
[d]: https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9
[e]: https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22

[f]: https://github.com/r-pufky/ansible_ufw/blob/main/LICENSE
[g]: https://github.com/r-pufky/ansible_collection_deb
[i]: https://github.com/r-pufky/ansible_ufw/blob/main/meta/main.yml
[j]: https://github.com/r-pufky/ansible_ufw/tree/main/defaults/main/main.yml
[k]: https://github.com/r-pufky/ansible_ufw/tree/main/defaults/main/ufw_group.yml
[l]: https://github.com/r-pufky/ansible_ufw/tree/main/defaults/main/ufw_host.yml