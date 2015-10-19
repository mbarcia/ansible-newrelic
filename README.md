# drupsible-newrelic

Drupsible role to manage the New Relic Server Agent (System Monitor Daemon) v2.2+. For a detailed configuration docs see [Configuring Servers for Linux](https://docs.newrelic.com/docs/servers/new-relic-servers-linux/installation-configuration/configuring-servers-linux)

## Requirements

This role requires Ansible 1.8 or higher and platforms listed in the metadata file.

It needs to be run as root with something like become:yes in your playbook

>  roles:
>   - { role: drupsible-newrelic, tags: newrelic, become: yes }

## Role Variables

The variables that can be passed to this role and a brief description about them are as follows

    # License key
    newrelic_license_key: ab2fa361cd4d0d373833cad619d7bcc424d27c16
    
    # Log level (error, warning, info, verbose, debug, verbosedebug)
    newrelic_loglevel: info
    
    # Log file location
    newrelic_logfile: /var/log/newrelic/nrsysmond.log
    
    # Proxy server. Default False
    newrelic_proxy: fred:secret@proxy.mydomain.com:8181
    
    # Use SSL for all communication. Default true
    newrelic_ssl: "true"
    
    # SSL CA Bundle path. Default omit
    newrelic_ssl_ca_bundle: 
    
    # SSL CA Path. Default False
    newrelic_ssl_ca_path: /etc/ssl/certs

    # Disable Docker. Default False
    newrelic_disable_docker: "false"
    
    # Docker connection. Default /var/run/docker.sock
    newrelic_docker_connection: '/var/run/docker.sock'

    # Pid file location
    newrelic_pidfile: /var/run/newrelic/nrsysmond.pid
    
    # Collector hostname
    newrelic_collector_host: collector.newrelic.com

    # New Relic labels. Default none
    newrelic_labels: "Server:One;Data Center:Primary;"

    # New Relic hostname. Default hostname
    newrelic_hostname: "{{ ansible_hostname }}"

    # Ignore reclaimable memory. Default True
    newrelic_ignore_reclaimable: "true"

    # Disable NFS. Default False
    newrelic_disable_nfs: "false"
    
## Examples

### Paramaterized Role

    ---
    - hosts: all
      roles:
        - { role: newrelic, newrelic_license_key: ab2fa361cd4d0d373833cad619d7bcc424d27c16 }

### Vars

    ---
    - hosts: all
      vars:
        newrelic_license_key: ab2fa361cd4d0d373833cad619d7bcc424d27c16
      roles:
        - newrelic

### Group vars

#### group_vars/production

    ---
    newrelic_license_key: ab2fa361cd4d0d373833cad619d7bcc424d27c16

#### site.yml

    ---
    - hosts: all
      roles:
        - newrelic

## Credits
Originally forked from https://github.com/sivel/ansible-newrelic.
