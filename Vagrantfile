# -*- mode: ruby -*-
# vi: set ft=ruby :

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
  config.vm.box = "ubuntu/bionic64"

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
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network "private_network", ip: "192.168.99.100"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
       vb.memory = "4096"
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
  config.vm.provision "shell", inline: <<-SHELL
    # Install Vim
    sudo apt-get remove --assume-yes vim-tiny
    sudo apt-get update
    sudo apt-get install --assume-yes vim
  SHELL
  config.vm.provision "shell", inline: <<-SHELL
    # Install docker
    export DEBIAN_FRONTEND=noninteractive
    sudo apt-get -y update
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
    sudo apt-get -y update
    sudo apt-cache policy docker-ce
    sudo apt-get -y install docker-ce
    sudo systemctl docker start
    docker -v
    sudo usermod -aG docker vagrant
  SHELL
  config.vm.provision "shell", inline: <<-SHELL
    # Install Ansible
    sudo apt-get install python -y
    sudo apt-get update
    sudo apt-get install software-properties-common
    sudo apt-add-repository --yes --update ppa:ansible/ansible
    sudo apt-get update  
    sudo apt-get install ansible -y
    ansible --version
  SHELL
  config.vm.provision "shell", inline: <<-SHELL
    # Install Gitlab
    sudo apt update
    sudo apt install ca-certificates curl openssh-server postfix
    cd /tmp
    curl -LO https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh
    less /tmp/script.deb.sh
    sudo bash /tmp/script.deb.sh
    sudo EXTERNAL_URL="http://192.168.99.100:9100" apt-get install gitlab-ce
  SHELL
  config.vm.provision "shell", inline: <<-SHELL
    # Install Gitlab-CI-Runners
    curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh -o /tmp/gl-runner.deb.sh
    less /tmp/gl-runner.deb.sh
    sudo bash /tmp/gl-runner.deb.sh
    sudo EXTERNAL_URL="http://192.168.1.99:9100" apt-get install gitlab-runner
  SHELL
  config.vm.provision "shell", inline: <<-SHELL
    # Install Pelican
    sudo apt-get update -y
    sudo apt-get install -y pelican
  SHELL
end
