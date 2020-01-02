# -*- mode: ruby -*-
# vi: set ft=ruby :

CENTOS_COUNT = 1

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox"

  if CENTOS_COUNT > 0 then
    (1..CENTOS_COUNT).each do |i|
      hostname = "centos%02d" % i
      config.vm.define hostname do |centos|
        # CentOS 7
        # https://app.vagrantup.com/generic/boxes/centos7
        # https://github.com/lavabit/robox/
        centos.vm.box = "generic/centos7"
        centos.vm.hostname = hostname
        centos.vm.network :private_network, ip: "192.168.56.#{i + 40}"
        centos.vm.synced_folder ".vagrant_shared", "/home/vagrant/shared", disabled: true
        centos.vm.provider :virtualbox do |v|
          v.gui = false
          v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
          v.customize ["modifyvm", :id, "--memory", 512]
          v.customize ["modifyvm", :id, "--name", hostname]
        end
        centos.vm.provision "shell", inline: "echo \"IPs: $(hostname -I)\"", keep_color: true
      end
    end
  end

end
