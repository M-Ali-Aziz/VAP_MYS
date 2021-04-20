# -*- mode: ruby -*-
# vi: set ft=ruby :

#============================= VARIABLES =================================
# BOX use Ubuntu 18.04 LTS 64 bit
BOX = "geerlingguy/ubuntu1804"

# Private network ip number
IP = "10.1.0.10"

# Shared folder to the guest VM
HOST_FOLDER_PROJECT = "project"
GUEST_FOLDER_PROJECT = "/var/www/project"

# Customize VB
VB_NAME = "mys_vagrant"
MEMORY = 5000
CPU = 5

# Provisioning paths
# SHELL_PATH = "provisioning/provision.sh"
ANSIBLE_PLAYBOOK_PATH = "provision/ansible/playbook.yml"

#============================= CONFIGURATION =================================
# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = BOX

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: IP
  # config.vm.hostname = "myhost.local"
  # config.vm.network "private_network", ip: "192.168.33.10", hostname: true

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "host_machine/", "/guest/machine"
  config.vm.synced_folder HOST_FOLDER_PROJECT, GUEST_FOLDER_PROJECT, owner: "www-data", group: "www-data", mount_options:['dmode=775', 'fmode=775']
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # View the documentation for the provider you are using for more
  # information on available options.
  config.vm.provider "virtualbox" do |vb|
    # Virtual Machine Name
    vb.name = VB_NAME
    # Customize the amount of memory & cpu on the VM:
    vb.memory = MEMORY
    vb.cpus = CPU
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  # config.vm.provision :shell, path: SHELL_PATH
  # ANSIBLE
  # Run Ansible from the Vagrant VM
  config.vm.provision :ansible_local do |ansible|
    ansible.playbook = ANSIBLE_PLAYBOOK_PATH
    ansible.extra_vars = { ansible_python_interpreter: "/usr/bin/python3" }
#     ansible.install_mode = "pip"
#     ansible.pip_install_cmd = "sudo apt-get install -y python3-distutils && curl -s https://bootstrap.pypa.io/get-pip.py | sudo python3"
#     ansible.version = "latest"
#     ansible.verbose = true
#     ansible.tags = ["common","vhost"]
#     ansible.tags = "mariadb"
  end
end
