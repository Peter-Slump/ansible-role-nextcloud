# Ansible role Owncloud

Version: 0.0.2

Supported OS: Ubuntu

Ansible role Owncloud

- Uses PostgreSQL as database
- Runs in an own PHP pool

## Role variables
```

owncloud_version: '9.1.4'
owncloud_sha256sum: '1bf62c5e665a98f8c82fbeb2fcc5d2aa2bd3157b0cad2a93000a8d72114ca547'
owncloud_download_url: https://download.owncloud.org/community/owncloud-{{ owncloud_version }}.tar.bz2

owncloud_group: owncloud
owncloud_user: owncloud
owncloud_home: /home/{{ owncloud_user }}

owncloud_data_path: /var/data/owncloud/{{ owncloud_user }}/
owncloud_deploy_path: '{{ owncloud_home }}'

owncloud_dbname: '{{ owncloud_user }}'
owncloud_dbuser: '{{ owncloud_user }}'
owncloud_dbhost: 'localhost'
owncloud_dbpass: 'ChangeMe'

owncloud_hostname: owncloud.example.com

owncloud_use_self_signed_ssl: False
owncloud_use_letsencrypt: False

# Config settings
# The following settings should be supplied in a secure way:
owncloud_config_passwordsalt: 'NotVerySecretPasswordSalt'
# owncloud_config_passwordsalt: ' **  Some secret salt ** '
owncloud_config_secret: 'NotVerySecretConfigSecret'
# owncloud_config_secret: ' ** Some secret ** '
# owncloud_config_adminpass: ' ** Some secret password for the admin user ** '
owncloud_config_adminpass: 'NotVerySecretAdminPassword'
owncloud_config_adminlogin: 'admin'

owncloud_config_trusted_domains: [ "{{ owncloud_hostname }}" ]
owncloud_config_datadirectory: "{{ owncloud_data_path }}"
owncloud_config_overwrite_cli_url: "https://{{ owncloud_hostname }}"
owncloud_config_dbname: "{{ owncloud_dbname }}"
owncloud_config_dbuser: "{{ owncloud_dbuser }}"
owncloud_config_dbpassword: "{{ owncloud_dbpass }}"
owncloud_config_dbhost: "{{ owncloud_dbhost }}"

owncloud_php_port: 9001

# At what time cron should execute background jobs
owncloud_cron_minute: '*/15'

# Max upload size set in Nginx and PHP7.0, with amount as M or G
owncloud_upload_size: '10G'

# Output buffering set in PHP 7.0, with amount set in megabytes
owncloud_php_output_buffering: '128'

# Max children processes to run in php-fpm
owncloud_php_max_children: '50'
```

## Example
```
- hosts: all
  roles:
   - role: owncloud
     owncloud_hostname: owncloud.example.com
```
