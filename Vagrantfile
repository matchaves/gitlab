# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/focal64"
  config.vm.hostname = "gitlab.devops"
  config.vm.define "gitlab"
  

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end


  config.vm.network "public_network", bridge: "wlp8s0", ip: "192.168.50.220"


  #
   config.vm.provider "virtualbox" do |vb|
 
     vb.memory = "4000"
     vb.cpus = "3"
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
