# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.require_version ">= 1.7.0"

Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "7168"
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.become = true
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
    ansible.extra_vars = { 
      ansible_ssh_user: 'vagrant'
      # ansible_python_interpreter: "/usr/bin/python3"
    }
    ansible.sudo = true
    # ansible.inventory_path = "ansible-role-httpd/tests/inventory"
  end

end
