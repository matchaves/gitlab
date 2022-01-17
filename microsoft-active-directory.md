# Samba4 como Active Directory

To enable LDAP integration you need to add your LDAP server settings in /etc/gitlab/gitlab.rb

```bash
gitlab_rails['ldap_enabled'] = true
gitlab_rails['prevent_ldap_sign_in'] = false
gitlab_rails['ldap_servers'] = YAML.load <<-EOS
main: # 'main' is the GitLab 'provider ID' of this LDAP server
  label: 'GitLab Samba4 AD'
  host: '192.168.56.5'
  port: 389 # 389 or 636
  uid: 'sAMAccountName'
  bind_dn: 'gitlab-user@linuxpro.local'
  password: 'Linuxpro123456'
  encryption: 'start_tls' # "start_tls" or "simple_tls" or "plain"
  verify_certificates: false
  smartcard_auth: false
  active_directory: true
  allow_username_or_email_login: false
  lowercase_usernames: false
  base: 'dc=linuxpro,dc=local'
  user_filter: '(memberof=cn=gitlab,dc=linuxpro,dc=local)'
  #user_filter: '(|(memberof=cn=gitlab,dc=linuxpro,dc=local)(memberof=cn=iss_devops,dc=linuxpro,dc=local))'
  attributes:
    username: ['uid', 'userid', 'sAMAccountName']
    email:    ['mail', 'email', 'userPrincipalName']
    name:       'cn'
    first_name: 'givenName'
    last_name:  'sn'
EOS
```


## Active Directory 2008R2 ou Superior sem SSL

To enable LDAP integration you need to add your LDAP server settings in /etc/gitlab/gitlab.rb

```bash
gitlab_rails['ldap_enabled'] = true
gitlab_rails['prevent_ldap_sign_in'] = false
gitlab_rails['ldap_servers'] = YAML.load <<-EOS
main: # 'main' is the GitLab 'provider ID' of this LDAP server
  label: 'GitLab AD'
  host: '192.168.56.5'
  port: 389
  uid: 'sAMAccountName'
  bind_dn: 'gitlab-user@linuxpro.local'
  password: 'Linuxpro123456'
  encryption: 'plain'
  verify_certificates: false
  smartcard_auth: false
  active_directory: true
  allow_username_or_email_login: false
  lowercase_usernames: false
  base: 'dc=linuxpro,dc=local'
  user_filter: '(memberof=cn=gitlab,dc=linuxpro,dc=local)'
  attributes:
    username: ['uid', 'userid', 'sAMAccountName']
    email:    ['mail', 'email', 'userPrincipalName']
    name:       'cn'
    first_name: 'givenName'
    last_name:  'sn'
EOS
```


## Active Directory 2008R2 ou Superior com SSL

To enable LDAP integration you need to add your LDAP server settings in /etc/gitlab/gitlab.rb

```bash
gitlab_rails['ldap_enabled'] = true
gitlab_rails['prevent_ldap_sign_in'] = false
gitlab_rails['ldap_servers'] = YAML.load <<-EOS
main: # 'main' is the GitLab 'provider ID' of this LDAP server
  label: 'GitLab AD'
  host: '192.168.56.5'
  port: 636
  uid: 'sAMAccountName'
  bind_dn: 'gitlab-user@linuxpro.local'
  password: 'Linuxpro123456'
  encryption: 'start_tls'
  verify_certificates: false
  smartcard_auth: false
  active_directory: true
  allow_username_or_email_login: false
  lowercase_usernames: false
  base: 'dc=linuxpro,dc=local'
  user_filter: '(memberof=cn=gitlab,dc=linuxpro,dc=local)'
  attributes:
    username: ['uid', 'userid', 'sAMAccountName']
    email:    ['mail', 'email', 'userPrincipalName']
    name:       'cn'
    first_name: 'givenName'
    last_name:  'sn'
EOS
```


## Testando o acesso ao Active Directory

```bash
gitlab-ctl reconfigure
gitlab-rake gitlab:ldap:check
```

## Links

- https://docs.gitlab.com/ee/administration/auth/ldap/