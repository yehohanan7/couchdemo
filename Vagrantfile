# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"
  config.vm.box = "precise32"
  config.vm.network "private_network", ip: "192.168.5.5"
  config.vm.synced_folder ".", "/couchdemo"
  config.vm.network "forwarded_port", guest: 15986, host: 15986
  config.vm.network "forwarded_port", guest: 15984, host: 15984
  config.vm.network "forwarded_port", guest: 25986, host: 25986
  config.vm.network "forwarded_port", guest: 25984, host: 25984
  config.vm.network "forwarded_port", guest: 35986, host: 35986
  config.vm.network "forwarded_port", guest: 35984, host: 35984
  
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision :ansible do |ansible|
    ansible.verbose = "vvvv"
    ansible.extra_vars = {
      proxy_user: "user",
      proxy_password: "password",
      proxy_host: "host",
      proxy_port: "port"
    }
    ansible.sudo = true
    ansible.playbook = "scm/ansible/site.yml"
    ansible.inventory_path = "hosts"
    ansible.limit = "local"
  end

end
