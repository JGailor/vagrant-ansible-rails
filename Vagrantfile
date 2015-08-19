# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.define "rails01" do |machine|
    machine.vm.box = "ubuntu/trusty64"
    machine.vm.hostname = "rails01"
    machine.vm.network "private_network", ip: "192.168.66.66"
  end
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "rails_server.yml"
    #ansible.verbose = 'vvvv'
    ansible.groups = {
      "webservers" => ["rails01"],
      "databases" => ["rails01"]
    }
  end
end
