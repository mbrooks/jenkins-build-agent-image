# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "generic/ubuntu2204"
  
    config.vm.network "private_network", type: "dhcp" 

      config.vm.provider :libvirt do |libvirt|
        libvirt.cpus = 1
        libvirt.memory = "1024"
    end

    # Enable provisioning with a shell script. Additional provisioners such as
    # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
    # documentation for more information about their specific syntax and use.
    config.vm.provision "shell", inline: <<-SHELL
       apt-get update
       apt-get install -y build-essential apt-transport-https ca-certificates curl gnupg-agent software-properties-common openjdk-11-jre vim

       # install docker and docker-compose
       curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
       add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
       apt-get update
       apt-get install -y docker-ce
       systemctl enable docker
       systemctl start docker
       curl -L https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
       chmod +x /usr/local/bin/docker-compose
       usermod -aG docker vagrant

       # setup jenkins directory
       mkdir /var/jenkins
       chown -R vagrant: /var/jenkins
    SHELL
end
