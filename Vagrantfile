# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
config.vm.box = "trusty64"
#config.vm.box_check_update = false


  config.vm.define "web1" do |web1|
    web1.vm.hostname = 'web1'
    web1.vm.network :private_network, ip: "192.168.56.101"
    web1.vm.network :forwarded_port, guest: 80, host: 8010
    web1.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 256]
      v.customize ["modifyvm", :id, "--name", "web1"]
    end
  end

  config.vm.define "web2" do |web2|
    web2.vm.hostname = 'web2'
    web2.vm.network :private_network, ip: "192.168.56.102"
    web2.vm.network :forwarded_port, guest: 80, host: 8020
    web2.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 256]
      v.customize ["modifyvm", :id, "--name", "web2"]
    end
  end

  config.vm.define "lb" do |lb|
    lb.vm.hostname = 'lb'
    lb.vm.network :private_network, ip: "192.168.56.103"
    lb.vm.network :forwarded_port, guest: 80, host: 8000
    lb.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "lb"]
    end
  end

  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.hostname = 'jenkins'
    jenkins.vm.network :private_network, ip: "192.168.56.104"
    jenkins.vm.network :forwarded_port, guest: 8080, host: 8080
    jenkins.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "jenkins"]
    end
  end

  config.vm.provision :ansible do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
    ansible.inventory_path ="hosts" 
  end
end

#Vagrant.configure(2) do |config2|
 # config2.vm.provision :ansible do |ansible|
  #  ansible.verbose = "v"
   # ansible.playbook = "playbook.yml"
    #ansible.inventory_path ="hosts"
 # end
#end
