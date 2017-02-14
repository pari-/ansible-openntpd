# openntpd

An Ansible role which installs and configures OpenNTPd

## Requirements

Currently this role is developed for and tested on Debian GNU/Linux (release: jessie). It is assumed to work on other Debian distributions as well.

Ansible version in use for development: 2.2.0

## Example

```yaml
- hosts: openntpd-servers
  roles:
     - { role: openntpd }
```

In addition to that, you'll have to supply an `openntpd_configure_config`-dict, though (see below).

## Role Variables

Available variables are listed below, along with default values (see defaults/main.yml):

- `openntpd_configure_config_defaults`

  > Sane defaults which are applied to the configuration options in `openntpd_configure_config`
  >
  >

```yaml
openntpd_configure_config_defaults:
  weight:
    server: 1
    servers: 1
    sensor: 1
  rtable: 253
  correction: 0
  refid: none
  stratum: 1
```

- `openntpd_configure_config`

  > Main configuration dict, for an example - see the YAML below:
  >
  >

```yaml
openntpd_configure_config:
  listen_on:
    localhost:
      address: "127.0.0.1"
    all:
      address: "*"
      rtable: 4
  servers:
    ptbtim1.ptb.de:
      address: "ptbtime1.ptb.de"
    ptbtime2.ptb.de:
      address: "ptbtime2.ptb.de"
    ptbtime3.ptb.de:
      address: "ptbtime3.ptb.de"
      weight: 3
  sensors:
    mySensor1:
      device: "nmea0"
      correction: 70000
      refid: "GPS"
      stratum: 2
    mySensor2:
      device: "*"
```

### Role Internals

#### prerquisites

- `openntpd_prerequisites_supported_distribution_releases`
> A list of distribution releases this role supports.
>
> `['jessie']`

- `openntpd_prerequisites_apt_update_cache`

> Run the equivalent of apt-get update before the operation.
>
> `"yes"`

- `openntpd_prerequisites_apt_cache_valid_time`

> Update the apt cache if its older than the set value.
>
> `"3600"`

- `openntpd_prerequisites_package_list`

> The list of packages to be prerequisitesed.
>
> `[]`

#### install

- `openntpd_install_apt_update_cache`

> Run the equivalent of apt-get update before the operation.
>
> `"yes"`

- `openntpd_install_apt_cache_valid_time`

> Update the apt cache if its older than the set value.
>
> `"3600"`

- `openntpd_install_package_list`

> The list of packages to be installed.
>
> `['openntpd']`

#### configure

- `openntpd_configure_template_dest`

  > Path of OpenNTPd's configuration file.
  >
  > `"/etc/openntpd/ntpd.conf"`

- `openntpd_configure_service_name`

  > Name of the OpenNTPd service.
  >
  > `"openntpd"`

## Dependencies

None.

## License

MIT

## Author Information

* Patrick Ringl
