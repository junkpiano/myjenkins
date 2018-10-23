# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  # config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "private_network", ip: "192.168.33.11"
  # config.vm.network "public_network"
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false  
    vb.memory = "512"
  end

  # This is workaround for Ubuntu 18. By default, its nameserver is localhost, and that's the reason
  # that docker cannot access internet. https://superuser.com/a/1335054
  config.vm.provision "shell", inline: <<-SHELL
    ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
  SHELL

  config.vm.provision "docker" do |d|
    d.build_image '/vagrant/'
  end
end
