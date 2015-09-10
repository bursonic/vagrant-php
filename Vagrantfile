# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "10.11.0.2"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "../tao", "/var/www/tao", owner: "www-data", group: "www-data"

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

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "file", source: "config/database/init_pg.sql", destination: "/tmp/config/postgre/init_pg.sql"
  config.vm.provision "file", source: "config/nginx/tao.loc", destination: "/tmp/config/nginx/sites/tao.loc"
  config.vm.provision "file", source: "config/php/fpm-php.ini", destination: "/tmp/config/php/fpm-php.ini"
  config.vm.provision "file", source: "config/php/cli-php.ini", destination: "/tmp/config/php/cli-php.ini"
  config.vm.provision "file", source: "config/php/modules/xdebug.ini", destination: "/tmp/config/php/modules/xdebug.ini"

  config.vm.provision "shell", inline: <<-SHELL
  	sudo apt-get update
	sudo apt-get install -y git
	sudo apt-get install -y nginx
	sudo apt-get install -y php5 php5-fpm php5-cli
    sudo apt-get install -y php5-gd php5-pgsql php5-tidy php5-curl php-xml-parser
	sudo apt-get install -y php5-xdebug
	sudo apt-get install -y postgresql postgresql-client
	sudo apt-add-repository -y ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get install -y nodejs
    sudo apt-get install -y ruby
    sudo gem install sass
    sudo npm install -g grunt-cli

	sudo cp /tmp/config/nginx/sites/tao.loc /etc/nginx/sites-available/
	sudo ln -s /etc/nginx/sites-available/tao.loc /etc/nginx/sites-enabled/tao.loc
	
	sudo cp "/tmp/config/php/fpm-php.ini" /etc/php5/fpm/php.ini
	sudo cp "/tmp/config/php/cli-php.ini" /etc/php5/cli/php.ini
	sudo cp /tmp/config/php/modules/xdebug.ini /etc/php5/mods-available/xdebug.ini

	sudo service nginx reload
	sudo service php5-fpm reload
	
	cat /tmp/config/postgre/init_pg.sql | sudo -u postgres psql
  SHELL

end