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
  config.vm.box = "whiteblock/workshop"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  config.vm.network "forwarded_port", guest: 8000, host: 8000, host_ip: "127.0.0.1"
  config.vm.network "forwarded_port", guest: 8545, host: 8545, host_ip: "127.0.0.1"
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
    vb.memory = "2048"
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  $start = <<-START
#!/bin/bash
sudo docker run --rm -d --name genesis \
-v /home/vagrant/.ssh/id_rsa:/root/.ssh/id_rsa \
-v /home/vagrant/.ssh/id_rsa.pub:/root/.ssh/id_rsa.pub \
-v /home/vagrant/.ssh/authorized_keys:/root/.ssh/authorized_keys \
-e SSH_USER='vagrant' \
-e SSH_KEY='/root/.ssh/id_rsa' \
-e HANDLE_NODE_SSH_KEYS='true' \
-e NODES_PUBLIC_KEY=/root/.ssh/id_rsa.pub \
-e NODES_PRIVATE_KEY=/root/.ssh/id_rsa \
-e LISTEN='0.0.0.0:8000' \
--net=host \
gcr.io/whiteblock/genesis:dev-alpine
START
  config.vm.provision "start", type: "shell", inline: $start
end
