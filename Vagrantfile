# -*- mode: ruby -*-
# vi: set ft=ruby :
HACONIWA_VERSION = (ENV['HACONIWA_VERSION'] || '0.5.2')

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vbox|
    vbox.memory = "2048"
    vbox.cpus   = 4
  end

  config.vm.synced_folder ".", "/vagrant", type: "rsync",
                          rsync__exclude: ".git/"

  config.vm.provision "shell", inline: <<-SHELL
    { haconiwa version | grep -q #{HACONIWA_VERSION} } && exit 0 || true

    apt-get update
    curl -s https://packagecloud.io/install/repositories/udzura/haconiwa/script.deb.sh | bash
    apt-get -y install haconiwa=#{HACONIWA_VERSION}-1

    mkdir -p /var/log/haconiwa
    chown haconiwa: /var/log/haconiwa

    apt-get -y install lxc lxc-templates
  SHELL
end
