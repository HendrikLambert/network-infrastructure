# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "vyos/current"
  
  # vagrant-vyos plugin handles SSH key insertion automatically
  config.ssh.insert_key = true
  
  # WAN Interface - Bridged to host network with static IP
  config.vm.network "public_network",
    ip: "192.168.178.250",
    mac: "080027000001"

  # LAN Interface - Private network with static IP, configured by vagrant-vyos plugin
  config.vm.network "private_network",
    ip: "192.168.50.1",
    virtualbox__intnet: "vyos_lan",
    mac: "080027000002"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "512"
    vb.cpus = 1
    vb.name = "vyos-router"
    
    # Enable promiscuous mode for routing
    vb.customize ["modifyvm", :id, "--nicpromisc2", "allow-all"]
    vb.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"]
  end

  # Ansible provisioning for VyOS configuration
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/vyos-playbook.yml"
    ansible.inventory_path = "ansible/inventory.ini"
    ansible.limit = "vyos"
    ansible.compatibility_mode = "2.0"
  end

end
