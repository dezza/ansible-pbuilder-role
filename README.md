# uchida.pbuilder

[![Ansible Role](https://img.shields.io/ansible/role/5966.svg)](https://galaxy.ansible.com/detail#/role/5966)
[![CircleCI](https://img.shields.io/circleci/project/uchida/ansible-pbuilder-role.svg)](https://circleci.com/gh/uchida/ansible-pbuilder-role)
[![License](https://img.shields.io/github/license/uchida/ansible-pbuilder-role.svg)](https://tldrlegal.com/license/creative-commons-cc0-1.0-universal)

ansible role to install pbuilder, clean room package builder for Debian based distributions.
In addition, this role creates basetgz and its config file for several distributions and CPU architectures eg. debian-sid-amd64, ubuntu-trusty-i386, raspbian-jessie-armhf.

## Role Variables

Available variables are listed below, along with default values:

```yaml
pbuilder_base: debian
pbuilder_dist: sid
pbuilder_arch: amd64
pbuilder_config: /etc/pbuilder.d/{{ pbuilder_base }}-{{ pbuilder_dist }}-{{ pbuilder_arch }}
pbuilder_update: no
```

`pbuilder_base` is a variable to specify base Linux distribution, one of `debian`, `ubuntu` and `raspbian`.

`pbuilder_dist` is a variable to specify version by its codename, for example `sid` for debian or `trusty` for ubuntu.

`pbuilder_arch` is a variable to specify CPU architecture for builder image, when it does not match current architecture,
`qemu-debootstrap` command is used to emulate specified one.

`pbuilder_config` is a variable to specify path to pbuilder config file for created basetgz.

`pbuilder_update` is a variable to specify update basetgz or not, default is `no`, don't update.

## Example Playbooks

install pbuilder and creates debian-sid-amd64 basetgz

```yaml
- hosts: servers
  roles:
  - role: uchida.pbuilder
    pbuilder_base: debian
    pbuilder_dist: sid
    pbuilder_arch: amd64
```

install pbuilder and creates ubuntu-trusty-i386 and raspbian-jessie-armhf basetgzs and keep them up-to-date.

```yaml
- hosts: servers
  roles:
  - role: uchida.pbuilder
    pbuilder_base: ubuntu
    pbuilder_dist: trusty
    pbuilder_arch: i386
    pbuilder_update: yes
  - role: uchida.pbuilder
    pbuilder_base: raspbian
    pbuilder_dist: jessie
    pbuilder_arch: armhf
    pbuilder_update: yes
```

## License

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed)

dedicated to public domain by [contributors](https://github.com/uchida/packer-pbuilder/graphs/contributors).
