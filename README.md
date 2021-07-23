# Ansible Role: GitLab
[![Gitlab pipeline status (self-hosted)](https://img.shields.io/gitlab/pipeline/dubzland/ansible-role-gitlab/main?gitlab_url=https%3A%2F%2Fgit.dubzland.net)](https://git.dubzland.net/dubzland/ansible-role-gitlab/pipelines)
[![Ansible role](https://img.shields.io/ansible/role/49952)](https://galaxy.ansible.com/dubzland/gitlab)
[![Ansible role downloads](https://img.shields.io/ansible/role/d/49952)](https://galaxy.ansible.com/dubzland/gitlab)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/49952)](https://galaxy.ansible.com/dubzland/gitlab)
[![Liberapay patrons](https://img.shields.io/liberapay/patrons/jdubz)](https://liberapay.com/jdubz/donate)
[![Liberapay receiving](https://img.shields.io/liberapay/receives/jdubz)](https://liberapay.com/jdubz/donate)

Installs and configures the GitLab EE DevOps platform.

## Requirements

Ansible 2.2 or higher.

## Role Variables

Available variables are listed below, along with their default values (see
    `defaults/main.yml` for more info):

### General configuration
```yaml
gitlab_edition: gitlab-ee
gitlab_version: ""
gitlab_configuration_template: "etc/gitlab/gitlab.rbj2"
gitlab_domain: "gitlab"
gitlab_time_zone: "UTC"
gitlab_default_theme: 1
gitlab_external_url: "https://{{ gitlab_domain }}"
```

### Email configuration
```yaml
gitlab_email_enabled: false
gitlab_email_from: "gitlab@{{ gitlab_domain }}"
gitlab_email_display_name: "Gitlab"
gitlab_email_reply_to: "gitlab@{{ gitlab_domain }}"
```

### Nginx configuration
```yaml
gitlab_nginx_enable: true
gitlab_nginx_listen_port: ''
gitlab_nginx_listen_https: true
gitlab_nginx_redirect_http_to_https: true
gitlab_nginx_ssl_certificate: "/etc/gitlab/ssl/{{ gitlab_domain }}.crt"
gitlab_nginx_ssl_certificate_key: "/etc/gitlab/ssl/{{ gitlab_domain }}.key"
gitlab_nginx_create_self_signed_cert: true
gitlab_nginx_self_signed_cert_subject: "/C=US/ST=Mississippi/L=Hernando/O=IT/CN={{ gitlab_domain }}"
gitlab_nginx_ssl_ciphers: "ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256"
gitlab_nginx_ssl_protocols: "TLSv1.2 TLSv1.3"
gitlab_nginx_ssl_session_cache: "builtin:1000  shared:SSL:10"
gitlab_nginx_ssl_session_timeout: "5m"
gitlab_nginx_ssl_dhparam: "/etc/gitlab/ssl/dhparams.pem"
gitlab_nginx_listen_addresses: ""
```

### SMTP configuration
```yaml
gitlab_smtp_enabled: false
gitlab_smtp_address: "smtp-server"
gitlab_smtp_port: 465
gitlab_smtp_user_name: "smtp user"
gitlab_smtp_password: "smtppassword"
gitlab_smtp_domain: "{{ gitlab_domain }}"
gitlab_smtp_authentication: "login"
gitlab_smtp_enable_starttls_auto: true
gitlab_smtp_tls: false
gitlab_smtp_openssl_verify_mode: "none"
gitlab_smtp_ca_path: "/etc/ssl/certs"
gitlab_smtp_ca_file: "/etc/ssl/certs/ca-certificates.crt"
```

### Backup configuration
```yaml
gitlab_backups_enabled: true
gitlab_manage_backup_path: true
gitlab_backup_path: /var/opt/gitlab/backups
gitlab_backup_archive_permissions: 0644
gitlab_backup_pg_schema: 'public'
gitlab_backup_keep_time: 604800
```

### Registry configuration
```yaml
gitlab_registry_enabled: true
gitlab_registry_external_url: ""
gitlab_registry_listen_port: ""
gitlab_registry_listen_https: false
```

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: dubzland.gitlab
      vars:
        dubzland_gitlab_external_url: 'https://git.example.com'
```

## License

MIT

## Author

* [Josh Williams](https://codingprime.com)
