# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-'SCRIPT'
# all of this runs as root
apk add build-base python3
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.box = "generic/alpine310"

  # disables vagrant-proxyconf plugin when it is installed
  #config.proxy.enabled = false

  config.vm.network "forwarded_port", guest:22, host: 2220, id: "ssh"
  config.vm.network "forwarded_port", guest:5000, host:5000
  config.vm.network "forwarded_port", guest:5001, host:5001
  config.vm.network "forwarded_port", guest:5002, host:5002
  config.vm.network "forwarded_port", guest:5003, host:5003

  config.ssh.username = "vagrant"
  config.ssh.forward_agent = true
  config.ssh.private_key_path = "C:/Users/t917981/.ssh/adam-telus"
  config.vm.provision "file", source: "C:/Users/t917981/.ssh/adam-telus.pub", destination: "~/.ssh/authorized_keys"

  config.vm.provision "shell", inline: $script

end
