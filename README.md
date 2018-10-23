# devgateway.letsencrypt

Install and configure Letsencrypt, obtain certificates, and set up renewal using Systemd. This role
requires EPEL on RedHat OSes.

## Required Variables

### `le_domains`

The list of domains to obtain certificates for. For wildcard certificates, leading asterisk and dot
are required.

### `le_email`

Contact email for certificate notices.

## Optional Variables

### `le_certbot_environment`

A dictionary of environment variables to pass to certbot.

Default: ``` {} ```

### `le_config_dir`

The directory where Letsencrypt stores configs and keys.

Default: ``` /etc/letsencrypt ```

### `le_enable_timer`

Whether the renewal timer should be activated permanently and started immediately.

Default: *true*

### `le_log_file`

Path to Letsencrypt log file.

Default: ``` /var/log/letsencrypt/letsencrypt.log ```

### `le_packages`

A structure describing required packages for Certbot and its plugins by OS family.

Default:

    RedHat:
      certbot: certbot
      dns-route53: python2-certbot-dns-route53
    Debian:
      certbot: certbot
      dns-route53: python3-certbot-dns-route53


### `le_plugin`

Certbot plugin to obtain certificates with.

Default: ``` webroot ```

### `le_plugin_settings`

A dictionary of configurations for each plugin.

Default:

    webroot:
      directory: /etc/letsencrypt/public_html


### `le_service_requires`

Array of Systemd unit names that Letsencrypt service should also `Require`. It always additionally
requires `network-online.target`.

Default: `[]`

### `le_staging_mode`

Obtain a staging (invalid) version of the certificates.

Default: *false*

### `le_systemd_dir`

The directory for Systemd custom units.

Default: ``` /etc/systemd/system ```

### `le_unit_name`

The name for service and timer units of Letsencrypt.

Default: ``` update-letsencrypt ```

### `le_update_interval`

The interval for update timer, see `systemd.timer(5)` for syntax.

Default: ``` daily ```

## Playbook Example

    ---
    - hosts:
        - webserver
      tasks:
        - name: Configure Letsencrypt
          include_role:
            name: devgateway.letsencrypt
          vars:
            le_email: admin@example.org
            le_domains:
              - www.example.org
              - example.org


## License

GPLv3+

## Author Information

Copyright 2018, Development Gateway

