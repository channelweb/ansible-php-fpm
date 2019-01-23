PHP-FPM role
============

Simple ansible role to setup PHP FPM with minimal configuration.

Role Variables
--------------

Main role variables are `phpfpm_ini` providing php.ini settings and `phpfpm_pools` providing PHP-FTP pool settings.

See an example below.

```yaml
phpfpm_ini:
  - section: Date
    option: date.timezone
    value: Europe/Berlin

  - section: PHP
    option: upload_max_filesize
    value: 40M


phpfpm_pools:

  my_apps:
    prefix: /var/www/my_apps

    user: www-data
    group: www-data
    listen: /var/run/php/my-apps.sock
    listen.owner: www-data
    listen.group: www-data

    pm: dynamic
    pm.max_children: 100

    access.log: /var/log/php-my-apps-access.log
    slowlog: /var/log/php-my-apps-slow.log
    request_slowlog_timeout: "\"1s\""

    php_admin_value[error_log]: /var/log/php-my-apps-error.log
    php_admin_flag[log_errors]: on
```

License
-------

BSD
