# devgateway.letsencrypt

Configure Letsencrypt.

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

Variable description.

Default: ``` /etc/letsencrypt ```

### `le_enable_timer`

Variable description.

Default: *True*

### `le_log_file`

Variable description.

Default: ``` /var/log/letsencrypt/letsencrypt.log ```

### `le_packages`

Variable description.

Default:

* **RedHat**: {'certbot': 'certbot', 'route53': 'python2-certbot-dns-route53'}
* **Debian**: {'certbot': 'certbot', 'route53': 'python3-certbot-dns-route53'}


### `le_plugin`

Variable description.

Default: ``` webroot ```

### `le_plugin_settings`

Variable description.

Default:

* **webroot**: {'directory': '/etc/letsencrypt/public_html'}


### `le_service_requires`

Variable description.

Default:



### `le_staging_mode`

Variable description.

Default: *False*

### `le_systemd_dir`

Variable description.

Default: ``` /etc/systemd/system ```

### `le_unit_name`

Variable description.

Default: ``` update-letsencrypt ```

### `le_update_interval`

Variable description.

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

