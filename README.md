# Habilitando SSL no GitLab

## Raketasks

## Configurar o /etc/gitlab/gitlab.rb

```ruby
external_url = 'https://git.linuxpro.com.br'
nginx['ssl_certificate'] = "/etc/gitlab/ssl/git.linuxpro.com.br.crt"
nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/git.linuxpro.com.br.key"
```


## Executando o passo a passo.

```bash
rm -f /etc/gitlab/ssl/*.crt /etc/gitlab/ssl/*.key

cd /etc/gitlab/ssl/
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout $(hostname -f).key -out $(hostname -f).crt

chmod 755 /etc/gitlab/ssl
chmod 600 /etc/gitlab/ssl/*.crt /etc/gitlab/ssl/*.key
cp /etc/gitlab/ssl/*.crt /usr/local/share/ca-certificates/

update-ca-certificates
gitlab-ctl reconfigure
```


## Job de Backup GitLab

```bash
# Gitlab: backup_job
59 23 * * * gitlab-rake gitlab:backup:create >/var/log/gitlab_backup.log
30 23 * * * gitlab-ctl backup-etc /var/opt/gitlab/backups/ >/var/log/gitlab_etc.log
# Gitlab: backup_rotate
10 01 * * * find /var/opt/gitlab/backups -ctime +3 -exec rm -f  {} \;
```

## Backup usando Rsync

```bash
## apt-get -y install rsync
ssh-keygen -t rsa
ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.56.120
ssh root@192.168.56.120 'mkdir -p /backup/gitlab/'
rsync -avz --progress /var/opt/gitlab/backups/ root@192.168.56.120:/backup/gitlab/

# Rsync Backup Gitlab
## 10 02 * * * /usr/bin/rsync -avz --progress --delete /var/opt/gitlab/backups/ root@192.168.56.120:/backup/gitlab/
```


sudo  export EXTERNAL_URL="https://gitlab.example.com" GITLAB_ROOT_PASSWORD="root123" apt-get install gitlab-ee

export EXTERNAL_URL="http://gitlab.colabdevops.com" &&
export GITLAB_ROOT_PASSWORD="root123" &&
sudo apt-get install gitlab-ce=13.12

GITLAB_ROOT_PASSWORD="root123"


# docker swarm
export GITLAB_HOME=/srv/gitlab

docker swarm init

docker stack deploy --compose-file docker-compose.yml mystack

docker stack rm mystack

https://docs.gitlab.com/ee/install/docker.html

docker run --detach \
  --hostname gitlab.example.com \
  --env GITLAB_OMNIBUS_CONFIG="gitlab_rails['initial_root_password'] = 'rootroot123';" \
  --publish 443:443 --publish 5555:80 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume $GITLAB_HOME/config:/etc/gitlab \
  --volume $GITLAB_HOME/logs:/var/log/gitlab \
  --volume $GITLAB_HOME/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest

# register runner

gitlab-runner register \
  --non-interactive \
  --url "http://git.colab.com/" \
  --registration-token "g9-ts37Wd9zt1JsedfZp" \
  --executor "shell" \
  --docker-image alpine:latest \
  --description "docker-runner" \
  --tag-list "shell,aws" \
  --run-untagged="true" \
  --locked="false" \
  --access-level="not_protected"