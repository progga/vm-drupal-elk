# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  config.ssh.insert_key = false

  # VM for Elasticsearch, Logstash, Kibana (ELK), and Curator.
  config.vm.define "elk" do |elk|
    elk.vm.hostname = "elk.dev"
    elk.vm.box = "deb/jessie-i386"
    elk.vm.network "private_network", ip: "192.168.33.35"

    elk.vm.provider "virtualbox" do |vb|
      # The ELK stack needs more memory thanks to the JVM.
      vb.memory = 1152
    end

    elk.vm.provision "ansible" do |ansible|
      ansible.playbook = "the-ansible-files/elk-provision.yml"
    end
  end

  # VM for Drupal.
  config.vm.define "drupal" do |drupal|
    drupal.vm.hostname = "drupal.dev"
    drupal.vm.box = "deb/jessie-i386"
    drupal.vm.network "private_network", ip: "192.168.33.33"

    drupal.vm.provider "virtualbox" do |vb|
      vb.memory = 512
    end

    drupal.vm.provision "ansible" do |ansible|
      ansible.playbook = "the-ansible-files/drupal-provision.yml"
    end
  end
end
