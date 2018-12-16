# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/bionic64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  #config.vm.network "forwarded_port", guest: 8088, host: 8088

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  #config.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.10.15"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  #config.vm.synced_folder "../www_local", "/var/simplesamlphp"

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
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
  	apt-get update
     	apt-get remove -y apache2
        apt-get install -y nginx
	apt-get install -y php7.2
	sudo apt-get install -y php7.2-cli
	sudo apt-get install -y php-xml php-mbstring php-curl php-memcache php-ldap memcached php-fpm php-mysql
	sudo apt-get install -y mysql-server mysql-client
	sudo cat /vagrant/hosts > /etc/hosts 
	sudo mkdir -p /etc/nginx/ssl
	sudo hostname test.mymac.com
	sudo cat "test.mymac.com" > /etc/hostname
	sudo cp /vagrant/sam /etc/nginx/sites-available/sam
	sudo cp /vagrant/test.mymac* /etc/nginx/ssl/
	sudo ln -s /etc/nginx/sites-available/sam /etc/nginx/sites-enabled/sam
	sudo cp /vagrant/simplesamlphp-1.16.2.tar.gz /home/vagrant
	sudo tar xvfz simplesamlphp-1.16.2.tar.gz 
	sudo mkdir -p /var/simplesamlphp
	sudo mv -f /home/vagrant/simplesamlphp-1.16.2/* /var/simplesamlphp/
	sudo cp /vagrant/server.* /var/simplesamlphp/cert/
	sudo cp /vagrant/config* /var/simplesamlphp/config/
	sudo cp /vagrant/auths* /var/simplesamlphp/config/
	sudo cp /vagrant/saml* /var/simplesamlphp/metadata/
	sudo touch /var/simplesamlphp/modules/exampleauth/enable
	sudo touch /var/simplesamlphp/modules/sqlauth/enable
	sudo mysql   < /vagrant/dbuser.sql
	sudo mysql  -D simplesaml < /vagrant/example.sql
	sudo service nginx restart
   SHELL
end
