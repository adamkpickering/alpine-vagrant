# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-'SCRIPT'
# all of this runs as root

# basic development tools
apk add man-pages git git-doc vim openssh openssh-doc tmux bash bash-doc less \
	nmap nmap-doc curl curl-doc jq jq-doc tcpdump tcpdump-doc

# python
apk add python3 py3-pip build-base python3-dev openssl-dev libffi-dev
pip3 install --upgrade pip setuptools wheel requests credstash

# kubectl
curl -LOs "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod 755 kubectl
mv kubectl /usr/local/bin/kubectl

# ssh config
mkdir -p /home/vagrant/.ssh
printf 'Host github.com\n\tHostname ssh.github.com\n\tPort 443\n\tForwardAgent yes\n' > /home/vagrant/.ssh/config

# make sure .bashrc is run for login shells
printf 'if [ -f "$HOME/.bashrc" ]; then\n\t. "$HOME/.bashrc"\nfi\n' > /home/vagrant/.profile
SCRIPT

Vagrant.configure("2") do |config|

  config.vm.box = "generic/alpine312"

  # disables vagrant-proxyconf plugin when it is installed
  #config.proxy.enabled = false

  config.vm.network "forwarded_port", guest:22, host: 2220, id: "ssh"
  config.vm.network "forwarded_port", guest:5000, host:5000
  config.vm.network "forwarded_port", guest:5001, host:5001
  config.vm.network "forwarded_port", guest:5002, host:5002
  config.vm.network "forwarded_port", guest:5003, host:5003

  config.vm.provision "file", source: "C:/Users/t917981/.ssh/adam-telus.pub", destination: "~/.ssh/authorized_keys"

  config.vm.provision "shell", inline: $script

end
