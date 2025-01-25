# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "debian" do |debian|
    debian.vm.box = "generic/debian12"
    debian.vm.network "private_network", ip: "192.168.56.6"
    debian.vm.network :forwarded_port, guest: 22, host: 2230, host_ip: "0.0.0.0", id: "ssh", auto_correct: true
    debian.vm.network "public_network", bridge: "Realtek Gaming 2.5GbE Family Controller"
    config.vm.provider "virtualbox" do |vb|
      #vb.memory = "4096"
      #vb.cpus = 2
      vb.customize ["modifyvm", :id, "--usb-ohci", "on"]
      vb.customize ["modifyvm", :id, "--usb-ehci", "on"]
      vb.customize ["modifyvm", :id, "--x86-pae", "off"]
      vb.customize ["modifyvm", :id, "--audio-controller", "ac97"]
      vb.customize ["modifyvm", :id, "--audio-driver", "default"]
      vb.customize ["modifyvm", :id, "--mouse", "usb"]
      vb.customize ["modifyvm", :id, "--keyboard", "usb"]
    end   
  end

  # config.vm.define "rocky" do |rocky|
  #   rocky.vm.box = "generic/rocky9"
  #   rocky.vm.network "private_network", ip: "192.168.56.7"
  #   rocky.vm.network "public_network"
  # end

  # config.vm.define "rhel" do |rhel|
  #   rhel.vm.box = "generic/rhel9"
  #   rhel.vm.network "private_network", ip: "192.168.56.8"
  #   rhel.vm.network "public_network"
  # end

  # config.vm.define "centos" do |centos|
	# centos.vm.box = "eurolinux-vagrant/centos-stream-9"
  #   centos.vm.network "private_network", ip: "192.168.56.9"
  #   centos.vm.network "public_network"
  # end

  # config.vm.define "ubuntu" do |ubuntu|
  #   ubuntu.vm.box = "generic/ubuntu2310"
  #   ubuntu.vm.network "private_network", ip: "192.168.56.10"
  #   ubuntu.vm.network "public_network"
  # end

  config.vm.provision "file", source: "/home/#{ENV['USER']}/.ssh/id_rsa.pub", destination: "~/.ssh/me.pub"
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "main.yml"
    ansible.raw_arguments = [
      "--vault-password-file=./vars/.vault_pass"
    ]
  end
end
