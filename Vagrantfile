# Generated by Cyber Sandbox Creator 3.0.0
# https://gitlab.ics.muni.cz/muni-kypo-csc/cyber-sandbox-creator
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

ansible_groups = {
  "hosts" => ["attacker", "server", "client"], 
  "routers" => ["router"], 
  "ssh" => ["router", "attacker", "server", "client"], 
  "winrm" => [], 
  "ansible" => ["router", "attacker", "server", "client"], 
  "user-accessible" => ["attacker"]
}

Vagrant.configure("2") do |config|

  # Device(router): router
  config.vm.define "router" do |device|
    device.vm.hostname = "router"
    device.vm.box = "munikypo/debian-10"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.1.26.1",
      netmask: "255.255.255.0"
    device.vm.network "private_network",
      virtualbox__intnet: "internet-connection",
      ip: "100.100.100.1",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "router"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.galaxy_role_file = "provisioning/requirements.yml"
      ansible.galaxy_roles_path = "provisioning/roles"
      ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
      ansible.limit = "router"
    end
  end

  # Device(host): attacker
  config.vm.define "attacker" do |device|
    device.vm.hostname = "attacker"
    device.vm.box = "munikypo/kali"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.1.26.23",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "attacker"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.galaxy_role_file = "provisioning/requirements.yml"
      ansible.galaxy_roles_path = "provisioning/roles"
      ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
      ansible.limit = "attacker"
    end
  end

  # Device(host): server
  config.vm.define "server" do |device|
    device.vm.hostname = "server"
    device.vm.box = "munikypo/debian-10"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.1.26.9",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "server"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.galaxy_role_file = "provisioning/requirements.yml"
      ansible.galaxy_roles_path = "provisioning/roles"
      ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
      ansible.limit = "server"
    end
  end

  # Device(host): client
  config.vm.define "client" do |device|
    device.vm.hostname = "client"
    device.vm.box = "munikypo/debian-10"
    device.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 1
    end
    device.vm.synced_folder ".",
      "/vagrant",
      type: "rsync",
      rsync__exclude: ".git/"
    device.vm.network "private_network",
      virtualbox__intnet: "switch",
      ip: "10.1.26.4",
      netmask: "255.255.255.0"
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "preconfig/playbook.yml"
      ansible.groups = ansible_groups
      ansible.limit = "client"
    end
    device.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "provisioning/playbook.yml"
      ansible.groups = ansible_groups
      ansible.galaxy_role_file = "provisioning/requirements.yml"
      ansible.galaxy_roles_path = "provisioning/roles"
      ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path} --force"
      ansible.limit = "client"
    end
  end
end