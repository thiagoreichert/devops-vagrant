# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  config.vm.box = "centos/7"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 512
    vb.cpus = 1
  end

  # Configuração de máquina virtual para Serviço WEB 
  config.vm.define "web" do |web|
    web.vm.network "public_network", ip: "192.168.0.101"
    web.vm.synced_folder "./files", "/vagrant"
    web.vm.provision "shell", inline: <<-SHELL
      # yum update -y
      hostnamectl set-hostname vagrant-web
      cat /vagrant/key/vagrant-key.pub >> .ssh/authorized_keys
      yum install epel-release -y
      yum install net-tools mlocate vim nginx -y
      systemctl start nginx.service
      systemctl enable nginx.service
    SHELL
  end

  # Configuração de máquina virtual para Ansible
  config.vm.define "ansible" do |ansible|
    ansible.vm.network "public_network", ip: "192.168.0.102"
    ansible.vm.synced_folder "./files", "/vagrant"
    ansible.vm.provision "shell", inline: <<-SHELL
      # yum update -y
      hostnamectl set-hostname vagrant-ansible
      cat /vagrant/key/vagrant-key.pub >> .ssh/authorized_keys
      cp /vagrant/vagrant-key /home/vagrant
      chmod 600 /home/vagrant/vagrant-key
      chown vagrant:vagrant /home/vagrant/vagrant-key
      rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
      yum install net-tools mlocate vim ansible -y 
      ansible-playbook -i /vagrant/configs/ansible/hosts /vagrant/configs/ansible/playbook.yaml
    SHELL
  end

  # Configuração de máquina virtual para PHP 7.1
  config.vm.define "php" do |php|
    php.vm.network "public_network", ip: "192.168.0.103"
    php.vm.network "forwarded_port", guest:80, host:8080
    php.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 2
      vb.name = "VM_PHP_7"      
    php.vm.synced_folder "./files", "/vagrant"
    php.vm.provision "shell", inline: <<-SHELL
      # yum update -y
      hostnamectl set-hostname vagrant-php
      cat /vagrant/key/vagrant-key.pub >> .ssh/authorized_keys
      iptables -F
      rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
      rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
      
      yum install php71w-pdo php71w php71w-devel php71w-common php71w-gd php71w-pear /
               php71w-soap php71w-mbstring -y
      yum install net-tools mlocate vim nodejs httpd telnet wget -y 
      # Nodejs, npm e gulp
      curl --silent --location https://rpm.nodesource.com/setup_8.x | bash -
      curl -L https://npmjs.org/install.sh | sh
      npm install --global gulp-cli
      # Envoy
      export PATH=$PATH:/root/.config/composer/vendor/bin
      echo 'export PATH=$PATH:/root/.config/composer/vendor/bin' >> /etc/profile
      echo 'export PATH=$PATH:/root/.config/composer/vendor/bin' >> /root/.bash_profile
      # Yarn
      wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo
      yum install yarn -y
      # Compose
      curl -sS https://getcomposer.org/installer | php
      mv composer.phar /usr/local/bin/composer
      composer global require "laravel/envoy=~1.0"
    SHELL
  end

  # Configuração de máquina virtual para MYSQL 5.7
  config.vm.define "mysql" do |mysql|
    mysql.vm.network "public_network", ip: "192.168.0.104"
    mysql.vm.network "forwarded_port", guest:80, host:8081
    mysql.vm.synced_folder "./files", "/vagrant"
    mysql.vm.provision "shell", inline: <<-SHELL
      # yum update -y
      hostnamectl set-hostname vagrant-mysql
      cat /vagrant/key/vagrant-key.pub >> .ssh/authorized_keys
      rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
      rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
      yum install net-tools mlocate vim -y 
    SHELL
  end


end