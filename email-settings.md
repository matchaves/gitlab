# Configurar E-mail Externo no seu Servidor de GitLab

Configure /etc/gitlab/gitlab.rb

```bash
### Email Settings
gitlab_rails['gitlab_email_enabled'] = true
gitlab_rails['gitlab_email_from'] = 'gitlab@linuxpro.com.br'
gitlab_rails['gitlab_email_display_name'] = 'GitLab LinuxPro'
gitlab_rails['gitlab_email_reply_to'] = 'devops@linuxpro.com.br'
gitlab_rails['gitlab_email_subject_suffix'] = ''
gitlab_rails['gitlab_email_smime_enabled'] = false


### GitLab email server settings
###! Docs: https://docs.gitlab.com/omnibus/settings/smtp.html

gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.linuxpro.com.br"
gitlab_rails['smtp_port'] = 587
gitlab_rails['smtp_user_name'] = "gitlab@linuxpro.com.br"
gitlab_rails['smtp_password'] = "@linuxpro123456"
gitlab_rails['smtp_domain'] = "smtp.linuxpro.com.br"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_tls'] = false
gitlab_rails['smtp_openssl_verify_mode'] = 'none'



### Envio com o Gmail
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.gmail.com"
gitlab_rails['smtp_port'] = 587
gitlab_rails['smtp_user_name'] = "my.email@gmail.com"
gitlab_rails['smtp_password'] = "my-gmail-password"
gitlab_rails['smtp_domain'] = "smtp.gmail.com"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_tls'] = false
gitlab_rails['smtp_openssl_verify_mode'] = 'peer'
```

## Ativando as configurações de E-mail

```bash

gitlab-ctl reconfigure

## Testando o envio de email via console
# gitlab-rails console
# Notify.test_email('destination_email@address.com', 'Message Subject', 'Message Body').deliver_now
```

## Links

 - https://docs.gitlab.com/omnibus/settings/smtp.html
 - https://docs.gitlab.com/omnibus/settings/smtp.html#testing-the-smtp-configuration
