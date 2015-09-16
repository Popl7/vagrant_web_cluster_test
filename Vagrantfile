# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "https://github.com/kraksoft/vagrant-box-ubuntu/releases/download/14.10/ubuntu-14.10-amd64.box"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--cpus", "1", "--memory", "512"]
  end

  config.vm.provision :ansible do |ansible|
    ansible.inventory_path = "inventory"
    ansible.playbook = "site.yml"
  end

  config.vm.define "proxy" do |proxy|
    proxy.vm.network "forwarded_port", guest: 80, host: 8080
    proxy.vm.network "private_network", ip: "192.168.50.2"
    proxy.vm.hostname = "proxy.internal"
  end

  config.vm.define "mysql" do |mysql|
    mysql.vm.network "private_network", ip: "192.168.50.4"
    mysql.vm.hostname = "mysql.internal"
  end

  config.vm.define "web" do |web|
    web.vm.network "private_network", ip: "192.168.50.5"
    web.vm.hostname = "web.internal"
  end

end
