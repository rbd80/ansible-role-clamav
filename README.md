# Ansible Role: ClamAV

Installs ClamAV on RedHat/CentOS/Amazon and Debian/Ubuntu Linux servers.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    clamav_packages:
      - clamav
      - clamav-base
      - clamav-daemon

(Defaults for Debian/Ubuntu shown). List of packages to be installed for ClamAV operations.

    clamav_daemon_localsocket: /var/run/clamav/clamd.ctl
    clamav_daemon_config_path: /etc/clamav/clamd.conf

Path configuration for ClamAV daemon. These are hardcoded specifically for each OS family (Debian and Red Hat) and cannot be overidden.

    clamav_daemon_configuration_changes:
      - regexp: '^.*Example$'
        state: absent
      - regexp: '^.*LocalSocket .*$'
        line: 'LocalSocket {{ clamav_daemon_localsocket }}'

Changes to make to the configuration file that is read from when ClamAV starts. You need to at least comment the 'Example' line and open a LocalSocket (or `TCPSocket`, e.g. `3310` by default) to get the ClamAV daemon to run.

    clamav_daemon_state: started
    clamav_daemon_enabled: yes

Control whether the `clamav-daemon` service is running and/or enabled on system boot.

    clamav_freshclam_daemon_state: started
    clamav_freshclam_daemon_enabled: yes

Control whether the `clamav-freshclam` service is running and/or enabled on system boot.

## Dependencies

None.


## Example Playbook
```yaml
    - hosts: servers
      sudo: yes
      roles:
        - ansible-role-clamav 
```
## Requirements.yaml
 
```yaml
- src: git+https://github.com/rbd80/ansible-role-clamav.git
  version: master
```
## License

MIT / BSD

## Author Information
Updated to support Amazon
This role was sourced from [Jeff Geerling](https://www.jeffgeerling.com/).
