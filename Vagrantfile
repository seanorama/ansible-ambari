# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "puppetlabs/centos-6.5-64-nocm"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false

  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--cpus", "1", "--memory", "1024"]
  end

  config.vm.define "ambari" do |ambari|
    ambari.vm.network "private_network", ip: "192.168.50.3"
    ambari.vm.hostname = "ambari.localdomain"
  end

  config.vm.define "master1" do |master1|
    master1.vm.network "private_network", ip: "192.168.50.4"
    master1.vm.hostname = "master1.localdomain"
  end

  config.vm.define "master2" do |master2|
    master2.vm.network "private_network", ip: "192.168.50.5"
    master2.vm.hostname = "master2.localdomain"
  end

  config.vm.define "slave1" do |slave1|
    slave1.vm.network "private_network", ip: "192.168.50.6"
    slave1.vm.hostname = "slave1.localdomain"
  end

  config.vm.define "slave2" do |slave2|
    slave2.vm.network "private_network", ip: "192.168.50.7"
    slave2.vm.hostname = "slave2.localdomain"

    # An Ansible hack (https://github.com/mitchellh/vagrant/issues/1784).
    # In a multi-vm configuration, VM machines will be started according to
    # their declaration order. Inserting the Ansible declaration here, makes
    # sure that the provisioning process will be executed only after all the
    # VMs are up and running.
    slave2.vm.provision "ansible" do |ansible|
      ansible.inventory_path = "inventory/vagrant-virtualbox"
      ansible.verbose = "v"
#      ansible.raw_arguments = "--check"
      ansible.raw_arguments = "--private-key=~/.vagrant.d/insecure_private_key"
      ansible.sudo = true
      ansible.playbook = "site.yml"
      ansible.extra_vars = { ansible_ssh_user: 'vagrant' }

      # Disable default limit (required with Vagrant 1.5+)
      ansible.limit = 'all'
    end

  end

end
