Ansible SECURITY-TOOLS ![ansible-Securty-tools](https://img.shields.io/badge/ansible-Securty_tools-fd4526.svg)
=================


[Overview]: #overview
[Role description]: #role-description
[Supported OS]: #supported-os
[Requirements]: #requirements
[Dependancies]: #dependancies
[Variables Maldetect]: #variables-maldetect
[Tags]: #tags
[Change cron path]: #change-cron-path
[Logs Directory]: #logs-directory
[Variables Lynis]: #variables-lynis
[Extras configuration variables]: #Extras-configuration-variables
[Variables Clamav]: #variables-clamav


#### Table of Contents

1. [Overview][Overview]
2. [Role description][Role description]
3. [Requirements][Requirements]
4. [Dependancies][Dependancies]
5. [Supported OS][Supported OS]
6. [Variables Maldetect][Variables Maldetect]
    - [Tags][Tags]
    - [Change cron path][Change cron path]
    - [Logs Directory][Logs Directory]
7. [Variables Lynis][Variables Lynis]
   - [Tags][Tags]
   - [Extras configuration variables][Extras configuration variables]
8. [Variables Clamav][Variables Clamav]
   - [Tags][Tags]


## Overview

This role manage [Linux Malware Detect] (LMD), a malware scanner for Linux, [Lynis], a security auditing tool and [ClamAV],  an open source antivirus engine for detecting trojans, viruses, malware & other malicious threats.

## Role description

This role install and configure MALDETECT, Lynis and ClamAV.

## Requirements

 - `wget`


## Dependancies

None

## Supported OS

  ![Debian](https://img.shields.io/badge/Debian-Jessie|Wheezy-blue.svg)
  ![Ubuntu](https://img.shields.io/badge/Ubuntu-Trusty|xenial-blue.svg)



## Variables Maldetect


 Variables |  Type  | Default 
|---|---|---|
| maldet_email_alert | number | 0 |
| maldet_email_subj | string | maldet alert from $(hostname) |
| maldet_email_addr | string | you@domain.com |
| maldet_email_ignore_clean | number | 0 |
| maldet_quar_hits | number | 0 |
| maldet_quar_susp | number | 0 |
| maldet_quar_susp_minuid | number | 500 |
| maldet_maxdepth | number | 15 |
| maldet_minfilesize | number | 32 |
| maldet_maxfilesize | number | 768 |
| maldet_hexdepth | number | 61440 |
| maldet_hex_fifo_scan | number |  1 |
| maldet_hex_fifo_depth | number | 524288 |
| maldet_clamav_scan | number | 1 |
| maldet_public_scan | number | 0 |
| maldet_string_length_scan | number | 0 |
| maldet_string_length | number | 150000 |
| maldet_inotify_base_watches | number | 15360 |
| maldet_inotify_minuid | number | 500 |
| maldet_inotify_webdir | string | public_html |
| maldet_inotify_nice | number | 10 | The priority that monitoring process will run as [ -19 = high prio , 19 = low prio, default = 10 ]

### Tags

Selective execution of tasks.

TAG | DESCRIPTION |EXAMPLES
  ---|---|---
  maldetect | Run all tasks of this role | ```ansible-playbook playbooks/maldetect.yml --tags maldetect```
  maldetect_install | Install maldetect| ```ansible-playbook playbooks/maldetect.yml --tags maldetect_install```
  maldetect_config | Configure maldetect | ```ansible-playbook playbooks/maldetect.yml --tags maldetect_config```
### Change cron path

`Exemple:`

```yaml
 maldet_cron:
      - name: "Maldet cron Home and vhost / recent day = 1"
        paths: "/var/www/*/www/,/home/* 1"
        minute: "*/1"

```

### Logs Directory

**```Maldetect```** logs file symlink to `/var/log/maldetect/event_log`


## Variables Lynis

### Tags

Selective execution of tasks.

TAG | DESCRIPTION |EXAMPLES
  ---|---|---
  lynis | Run all tasks of this role | ```ansible-playbook playbooks/lynis.yml --tags lynis```
  lynis_install | Install Lynis | ```ansible-playbook playbooks/lynis.yml --tags lynis_install```
  lynis_configure | Configure Lynis | ```ansible-playbook playbooks/lynis.yml --tags lynis_configure```
  lynis_reinstall | reinstall Lynis (only when lynis_reinstall variable is set and == True) | ```ansible-playbook playbook/lynis.yml --tags lynis_reinstall" ```

### Extras configuration variables

Look at ```Audit customizing``` field in default.prf to see available variables to set.

`Exemple:`

```yaml
audit_custom_extras:
  - "config:connections_max_wait_state:50:"
  - "config:debian_skip_security_repository:yes:"
```
## Clamav

### Tags

Selective execution of tasks.

TAG | DESCRIPTION |EXAMPLES
  ---|---|---
  clamav | Run all tasks of this role | ```ansible-playbook playbooks/clamav.yml --tags clamav```
  clamav_install | Install clamav | ```ansible-playbook playbooks/clamav.yml --tags clamav_install```

