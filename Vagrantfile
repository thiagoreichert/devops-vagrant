# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  config.vm.box = "centos/7"

  # Configuração de máquina virtual para Serviço WEB 
  config.vm.define "web" do |web|
    web.vm.network "public_network", ip: "192.168.0.101"
    web.vm.provision "shell", inline: <<-SHELL
      # yum update -y
      hostnamectl set-hostname vagrant-web
      yum install epel-release -y
      yum install net-tools mlocate nginx -y
      systemctl start nginx.service
      systemctl enable nginx.service
    SHELL
  end

  # Configuração de máquina virtual para Ansible
  config.vm.define "ansible" do |ansible|
    ansible.vm.network "public_network", ip: "192.168.0.102"
    ansible.vm.provision "shell", inline: <<-SHELL
      # yum update -y
      hostnamectl set-hostname vagrant-ansible
      rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
      yum install net-tools mlocate ansible -y 
    SHELL
  end

  # Configuração de máquina virtual para PHP 7.1
  config.vm.define "php" do |php|
    php.vm.network "public_network", ip: "192.168.0.103"
    php.vm.network "forwarded_port", guest:80, host:8080
    php.vm.provision "shell", inline: <<-SHELL
      # yum update -y
      hostnamectl set-hostname vagrant-php
      iptables -F
      rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
      rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
      
      yum install php71w-pdo php71w php71w-devel php71w-common php71w-gd php71w-pear /
               php71w-soap php71w-mbstring -y
      yum install net-tools mlocate nodejs httpd telnet wget -y 
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

  # Configuração de máquina virtual para PHP-MYSQL 7.1
  config.vm.define "mysql" do |mysql|
    mysql.vm.network "public_network", ip: "192.168.0.104"
    mysql.vm.network "forwarded_port", guest:80, host:8081
    mysql.vm.provision "shell", inline: <<-SHELL
      # yum update -y
      hostnamectl set-hostname vagrant-mysql
      rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
      rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
      yum install net-tools mlocate php71w-mysql -y 
    SHELL
  end


end