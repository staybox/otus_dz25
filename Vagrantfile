# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"
  config.vm.box_check_update = false

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provision.yml"
  end

  config.vm.define "mailserver" do |mailserver|
    mailserver.vm.hostname = "mailserver.otus.local"
    mailserver.vm.network "private_network", ip: "192.168.50.5"
    mailserver.vm.network "forwarded_port", guest: 25, host: 20025
    mailserver.vm.network "forwarded_port", guest: 143, host: 20143
  end

end
