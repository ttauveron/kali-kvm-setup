# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'

Vagrant.configure("2") do |config|
  config.vm.box = "kalilinux/rolling"
  config.vm.hostname = "pwnbox"

  config.vm.define "pwnbox"
  config.vm.provider :libvirt do |libvirt|
    name = "pwnbox"
    libvirt.cpus=8
    libvirt.memory=15716

    libvirt.disk_bus       = "virtio"
    libvirt.driver         = "kvm"
    libvirt.graphics_type  = "spice"
    libvirt.nic_model_type = "virtio"
    libvirt.sound_type     = "ich6"
    libvirt.video_type     = "qxl"
    libvirt.channel :type  => 'spicevmc', :target_name => 'com.redhat.spice.0',     :target_type => 'virtio'
    libvirt.channel :type  => 'unix',     :target_name => 'org.qemu.guest_agent.0', :target_type => 'virtio'
    libvirt.random  :model => 'random'


  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/main.yml"
  end

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
  # config.vm.network "public_network"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  #config.vm.provision "ansible_local" do |ansible|
  #  ansible.playbook = "playbook.yml"
  #end
end
