# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  #config.vm.box = "geerlingguy/ubuntu1404"
  config.vm.box = "trusty64"
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # ELK server.
  config.vm.define "logs" do |logs|
    logs.vm.hostname = "logs"
    logs.vm.network :private_network, ip: "192.168.9.90"

    logs.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/elk/playbook.yml"
      ansible.inventory_path = "provisioning/elk/inventory"
      ansible.sudo = true
    end
  end

  # Web server.
  config.vm.define "webs" do |webs|
    webs.vm.hostname = "webs"
    webs.vm.network :private_network, ip: "192.168.9.91"

    webs.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/web/playbook.yml"
      ansible.inventory_path = "provisioning/web/inventory"
      ansible.sudo = true
    end
  end

 # OSSEC Server
  config.vm.define "ossec" do |ossec|
    ossec.vm.hostname = "ossec"
    ossec.vm.network :private_network, ip: "192.168.9.93"

    ossec.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/ossec/playbook.yml"
      ansible.inventory_path = "provisioning/ossec/inventory"
      ansible.sudo = true
    end
  end
 # Proxy Server 
  config.vm.define "proxy" do |proxy|
    proxy.vm.hostname = "proxy"
    proxy.vm.network :private_network, ip: "192.168.9.94"

    proxy.vm.provision :ansible do |ansible|
      ansible.playbook = "provisioning/proxy/playbook.yml"
      ansible.inventory_path = "provisioning/proxy/inventory"
      ansible.sudo = true
    end
  end

end
