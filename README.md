# Ansible role nextcloud

Version: 0.1.1

Supported OS: Ubuntu

Ansible role nextcloud

- Uses PostgreSQL as database
- Runs in an own PHP pool

## Role variables
```

nextcloud_version: '9.1.4'
nextcloud_sha256sum: '1bf62c5e665a98f8c82fbeb2fcc5d2aa2bd3157b0cad2a93000a8d72114ca547'
nextcloud_download_url: https://download.nextcloud.org/community/nextcloud-{{ nextcloud_version }}.tar.bz2

nextcloud_group: nextcloud
nextcloud_user: nextcloud
nextcloud_home: /home/{{ nextcloud_user }}

nextcloud_data_path: /var/data/nextcloud/{{ nextcloud_user }}/
nextcloud_deploy_path: '{{ nextcloud_home }}'

nextcloud_dbname: '{{ nextcloud_user }}'
nextcloud_dbuser: '{{ nextcloud_user }}'
nextcloud_dbhost: 'localhost'
nextcloud_dbpass: 'ChangeMe'

nextcloud_hostname: nextcloud.example.com

nextcloud_use_self_signed_ssl: False
nextcloud_use_letsencrypt: False

# Config settings
# The following settings should be supplied in a secure way:
nextcloud_config_passwordsalt: 'NotVerySecretPasswordSalt'
# nextcloud_config_passwordsalt: ' **  Some secret salt ** '
nextcloud_config_secret: 'NotVerySecretConfigSecret'
# nextcloud_config_secret: ' ** Some secret ** '
# nextcloud_config_adminpass: ' ** Some secret password for the admin user ** '
nextcloud_config_adminpass: 'NotVerySecretAdminPassword'
nextcloud_config_adminlogin: 'admin'

nextcloud_config_trusted_domains: [ "{{ nextcloud_hostname }}" ]
nextcloud_config_datadirectory: "{{ nextcloud_data_path }}"
nextcloud_config_overwrite_cli_url: "https://{{ nextcloud_hostname }}"
nextcloud_config_dbname: "{{ nextcloud_dbname }}"
nextcloud_config_dbuser: "{{ nextcloud_dbuser }}"
nextcloud_config_dbpassword: "{{ nextcloud_dbpass }}"
nextcloud_config_dbhost: "{{ nextcloud_dbhost }}"

nextcloud_php_port: 9001

# At what time cron should execute background jobs
nextcloud_cron_minute: '*/15'

# Max upload size set in Nginx and PHP7.0, with amount as M or G
nextcloud_upload_size: '10G'

# Output buffering set in PHP 7.0, with amount set in megabytes
nextcloud_php_output_buffering: '128'

# Max children processes to run in php-fpm
nextcloud_php_max_children: '50'
```

## Example
```
- hosts: all
  roles:
   - role: nextcloud
     nextcloud_hostname: nextcloud.example.com
```
