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

1. First you need to specify shared folder of the project
`config.vm.synced_folder "../tao", "/var/www/tao", owner: "www-data", group: "www-data"`
2. 
