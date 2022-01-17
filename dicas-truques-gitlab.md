# Dicas e Truques para o GitLab


## Acessando o console

```shell
cd /home/git/gitlab
sudo -u git -H bin/rails console -e production

# Ou
gitlab-rails console -e production
```

## Backups

```shell
## /home/git/gitlab/tmp/backups/
cd /home/git/gitlab
sudo -u git -H bundle exec rake gitlab:backup:create RAILS_ENV=production
su git -c 'bundle exec rake gitlab:backup:create RAILS_ENV=production'

# Ou
gitlab-rake gitlab:backup:create
```

## OpenSUSE 15.2

```
## Erro no VirtualBox
## Update Grub; /etc/default/grub, change resume=/dev/sdaX (SWAP sda)

grub2-mkconfig -o /boot/grub2/grub.cfg
```

Add SSL para CA interna

```shell
cp /etc/ssl/private/nexus.crt /usr/share/pki/trust/anchors/
update-ca-certificates -v
ls /var/lib/ca-certificates/openssl/
```

## Links

- https://docs.gitlab.com/ee/security/reset_root_password.html
- https://docs.gitlab.com/ce/update/upgrading_from_source.html
- https://stackoverflow.com/questions/13080643/switching-user-in-fabric
- https://klauslaube.com.br/2012/02/26/automatize-o-deploy-dos-seus-projetos-com-fabric.html
- https://www.youtube.com/watch?v=ZpZkKbZwPoA
- https://docs.gitlab.com/ce/update/
