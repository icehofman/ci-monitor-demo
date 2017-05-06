# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
 
  config.vm.box = "williamyeh/ubuntu-trusty64-docker"

  # Add forwarded ports docker-compose-ci
  config.vm.network "forwarded_port", guest: 8888, host: 8888
  config.vm.network "forwarded_port", guest: 9000, host: 9000
  config.vm.network "forwarded_port", guest: 5432, host: 5432
  config.vm.network "forwarded_port", guest: 8181, host: 8181

  # Add forwarded ports docker-compose-selenium
  config.vm.network "forwarded_port", guest: 4444, host: 4444

  # Add forwarded ports docker-compose-monitor
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 9090, host: 9090
  config.vm.network "forwarded_port", guest: 9093, host: 9093

  # Add forwarded ports docker-compose-logs
  config.vm.network "forwarded_port", guest: 9200, host: 9200
  config.vm.network "forwarded_port", guest: 9300, host: 9300
  config.vm.network "forwarded_port", guest: 24224, host: 24224
  config.vm.network "forwarded_port", guest: 5601, host: 5601

  config.vm.synced_folder ".", "/vagrant", disabled: false
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 6144
    v.cpus = 2
  end

  config.vm.provision "shell", inline: "swapoff -a"
  config.vm.provision "shell", inline: "fallocate -l 2G /swapfile"
  config.vm.provision "shell", inline: "chmod 600 /swapfile"
  config.vm.provision "shell", inline: "mkswap /swapfile"
  config.vm.provision "shell", inline: "swapon /swapfile"

  config.vm.provision "shell", run: "always" do |s|
    s.inline = "docker stop $(docker ps -a -q) -t 90 && docker rm $(docker ps -a -q) -f"
  end 

  config.vm.provision :docker

  # Install the plugin: vagrant plugin install vagrant-docker-compose
  config.vm.provision :docker_compose,
    yml: [
      "/vagrant/docker-compose-monitor.yml",
      "/vagrant/docker-compose-logs.yml",
      "/vagrant/docker-compose-ci.yml",
      "/vagrant/docker-compose-selenium.yml"      
    ],
    rebuild: true,
    run: "always"
   
end
