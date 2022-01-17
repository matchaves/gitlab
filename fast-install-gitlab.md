# Instalação Rápida do GitLab

## Requisitos para criar o Servidor do GitLab

- 1 Servidor Linux
- HD 120
- RAM 8GB
- 2 CPUs


## Instalando GitLab no Ubuntu 18.04

```bash

## Fix
## dpkg-reconfigure tzdata
## hostnamectl set-hostname git.domain.com
## echo "" >>/etc/hosts
## echo "git.domain.com" >/etc/hostname
## echo "192.168.X.10  git.domain.com" >>/etc/hosts
## echo "git.domain.com" > /proc/sys/kernel/hostname


apt-get update
apt-get install -y ca-certificates curl openssh-server postfix
apt-get install -y apt-transport-https gnupg2 software-properties-common

## Gitlab
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
EXTERNAL_URL="https://git.domain.com" apt-get install -y gitlab-ce


## sed -i "s|# letsencrypt\['enable'\] = nil|letsencrypt\['enable'\] = false|" /etc/gitlab/gitlab.rb
## apt-get update && apt-get -f install
```

## Instalando GitLab no CentOS 8

```bash

systemctl stop firewalld
systemctl disable firewalld

yum install -y curl policycoreutils-python openssh-server

yum install -y postfix
systemctl start postfix && systemctl enable postfix && systemctl status postfix

curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
EXTERNAL_URL="https://git.domain.com" yum install -y gitlab-ce

## gitlab-ctl reconfigure
```