drupsible-newrelic
==================

Drupsible role to manage the New Relic Server Agent (System Monitor Daemon) v2.2+. For a detailed configuration docs see [Configuring Servers for Linux](https://docs.newrelic.com/docs/servers/new-relic-servers-linux/installation-configuration/configuring-servers-linux).

If PHP-FPM is installed, this role will also install the [New Relic PHP agent](https://docs.newrelic.com/docs/agents/php-agent/getting-started/new-relic-php).

If debops.pki is installed, this role is able to setup TLS in LSM for connecting to Docker API.

Requirements
------------

This role DOES NOT require PHP-FPM (Fast Process Manager) to be present. But if it is, it will install New Relic's PHP agent (both PHP5 and PHP7 are supported).

This role DOES NOT require DebOps PKI (Private Key Infrastructure) to be present. But if it is, it will provide certificates to setup TLS in LSM's connection to Docker.

This role can be used indepedently and does NOT require Drupsible to run.

Example playbook
----------------

```
roles:
- { role: drupsible-newrelic, tags: [ role::newrelic ], become: yes }
```

Role Variables
--------------

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
    newrelic_hostname: "{{ ansible_hostname|d(inventory_hostname) }}"

    # Ignore reclaimable memory. Default True
    newrelic_ignore_reclaimable: "true"

    # Disable NFS. Default False
    newrelic_disable_nfs: "false"

License
-------

GNU General Public License v3

Author Information
------------------

Mariano Barcia - [https://github.com/mbarcia](https://github.com/mbarcia)

Credits
-------

Originally forked from https://github.com/sivel/ansible-newrelic.
