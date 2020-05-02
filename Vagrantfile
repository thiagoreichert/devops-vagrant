# -*- mode: ruby -*-
# vi: set ft=ruby :

# Configurando Vagrant versão 2:

Vagrant.configure("2") do |config|

  # Documentação https://docs.vagrantup.com.
  # Box = https://vagrantcloud.com/search.
  
  # Configurando o cents 7
  config.vm.box = "centos/7"

  # Atualização automática do Box. Recomendável 'false'.
  # config.vm.box_check_update = false

  # Criação de forwarded port para linkar uma porta do guest ao host. Esta configuraão é apenas privado.
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Criação de forwarded port com um IP específico, desta maneira impossibilita qualquer acesso público.
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Criação de private network, acessível apenas da máquina host, com IP estático.
  # config.vm.network "private_network", ip: "192.168.10.10"

  # Criação de private network, com IP definido pelo servidor DHCP do VirtualBox.
  # config.vm.network "private_network", type: "dhcp"

  # Criação de public network, associado a um bridged network.
  # Bridged networks faz a máquina aparecer fisicamente na rede local.
  config.vm.network "public_network", ip: "192.168.0.101"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
