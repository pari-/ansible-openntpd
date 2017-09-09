# openntpd

[![Build Status](https://travis-ci.org/pari-/ansible-openntpd.svg?branch=master)](https://travis-ci.org/pari-/ansible-openntpd)

An Ansible role which installs and configures OpenNTPd

<!-- toc -->

- [Requirements](#requirements)
- [Example](#example)
- [Role Variables](#role-variables)
- [Dependencies](#dependencies)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->

## Requirements

Currently this role is developed for and tested on Debian GNU/Linux (release: jessie). It is assumed to work on other Debian distributions as well.

Ansible version compatibility:

- __2.3.2.0__ (current version in use for development of this role) 
- 2.2.3.0
- 2.1.6.0
- 2.0.2.0

## Example

```yaml
---

- hosts: "all"
  vars:
    openntpd_config_options:
      listen_on:
        any:
          address: "*"
      servers:
        ptbtim1.ptb.de:
          address: "ptbtime1.ptb.de"
        ptbtime2.ptb.de:
          address: "ptbtime2.ptb.de"
        ptbtime3.ptb.de:
          address: "ptbtime3.ptb.de"
  roles:
    - role: "ansible-openntpd"
      tags:
        - "openntpd"
```

## Role Variables

Available variables are listed below, along with default values (see defaults/main.yml). They're generally prefixed with `openntpd_` (which I deliberately leave out here for better formatting).

variable | default | notes
-------- | ------- | -----
`cache_valid_time` | `3600` | `Update the apt cache if its older than the set value (in seconds)`
`config_file` | `/etc/openntpd/ntpd.conf` | `Absolute path to openntpd's configuration file`
`default_release` | `{{ ansible_distribution_release\|lower }}` | `The default release to install packages from`
`package_list` | `['openntpd']` | `The list of packages to be installed`
`pre_default_release` | `{{ openntpd_default_release }}` | `The default release to install packages (pre_package_list) from`
`pre_package_list` | `['apt-transport-https','ca-certificates']` | `The list of prerequisite packages to be installed`
`repo_list` | `[]` | `(additional) repository list`
`service_name` | `openntpd` | `Name of the (openntpd) service`
`supported_distro_list` | `['stretch']` | `A list of distribution releases this role supports`
`update_cache` | `yes` | `Run the equivalent of apt-get update before the operation`

## Dependencies

None

## License

MIT

## Author Information

* Patrick Ringl
