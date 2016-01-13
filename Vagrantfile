# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.define "graylog" do |graylog|
    graylog.vm.box = "mrlesmithjr/trusty64"
    graylog.vm.hostname = "graylog"

    graylog.vm.network :private_network, ip: "192.168.202.201"
    graylog.vm.network "forwarded_port", guest: 9000, host: 9000
    graylog.vm.network "forwarded_port", guest: 9200, host: 9200

    graylog.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
    end
  end
  config.vm.provision :shell, path: "provision.sh", keep_color: "true"
end
