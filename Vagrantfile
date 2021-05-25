# -*- mode: ruby -*-
# vi: set ft=ruby:

Vagrant.configure("2") do |config|
  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "centos/8"
    ansible.vm.hostname = "ansible"
    ansible.vm.network "private_network", ip: "172.69.128.3", virtualbox_intnet: true

    ansible.vm.provider "virtualbox" do |vb|
      vb.name = "ansible"
      vb.cpus = 2
      vb.memory = 1024
    end
    ansible.vm.provision "shell", path: "user.sh"
    ansible.vm.provision  "shell", run: "always", inline: <<-SHELL
      sudo dnf makecache -y
      sudo dnf install epel-release -y
      sudo dnf makecache -y
      sudo dnf install ansible -y
      sudo dnf install vim -y
      sudo dnf install tree -y
      echo "autocmd FileType yaml setlocal ai ts=2 sw=2 et" > /home/vagrant/.vimrc
    SHELL
  end

  config.vm.define "ubuntu-vm" do |vm1|
    vm1.vm.box = "ubuntu/focal64"
    vm1.vm.hostname = "ubuntu-vm"
    vm1.vm.network "private_network", ip: "172.69.128.15", virtualbox_intnet: true

    vm1.vm.provider "virtualbox" do |vb|
      vb.name = "ubuntu-vm"
      vb.cpus = 2
      vb.memory = 1024
    end
    vm1.vm.provision "shell", path: "user.sh"
  end

end
