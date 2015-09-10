# vagrant-php
Vagrant box with PHP preconfigured environment

## Preconfiguration

Edit Vagrant file first to meet your preferred setup. 
Anyway, default configuration also can be used.

There are three basic tweaks you may need to be done:
1. Host/guest shared folders
2. Web-stack project specific settings
3. Guest system NAT addess

### Project settings

* Specify shared folder of the project in your *Vagrantfile*

`config.vm.synced_folder "../tao", "/var/www/tao", owner: "www-data", group: "www-data"`

Good practice is to have separate shared folder per project. But you can share single web-root as well. 
Please note guest system owner and group settings.

* Add nginx server file per project

Nginx config files are located in *config/nginx* folder. You can use *tao.loc* file as a template for new projects.

* Add database initialisation

Add SQL file with database initialisation routines as user/database creation. You can use *config/database/inti_pg_tao.sql* as a template.

### Guest NAT settings

To define specific IP address of guest system, please edit this line in your *Vagrantfile*:

`config.vm.network "private_network", ip: "10.11.0.2"`
