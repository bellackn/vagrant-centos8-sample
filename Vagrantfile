# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
HOSTNAME = "foo"

# ssh port
SSH_PORT = 22022

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "centos/8"
  config.vm.hostname = HOSTNAME

  # define sync folders
  config.vm.synced_folder "./", "/home/vagrant/sample", create: false, type: "rsync", rsync__auto: true, rsync__args: ["--verbose", "--archive", "-z", "--copy-links"]

  # force auto update of VirtualBox guest additions
  config.vbguest.auto_update = true

  config.vm.provider "virtualbox" do |vb|
    # set vm name
    vb.name = HOSTNAME
  end

  # provision controlhost
  config.vm.provision "ansible_local" do |ansible|
    ansible.provisioning_path = "/home/vagrant/sample/"
    ansible.install_mode = "pip"
    ansible.version = "2.7.13"
    ansible.compatibility_mode = "2.0"
    ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3" }
    # playbook settings
    ansible.inventory_path = "inventory"
    ansible.playbook = "playbook.yml"
    ansible.limit = "all"
  end

end