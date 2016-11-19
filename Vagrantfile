# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network :forwarded_port, guest: 3306, host: 3306
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password'
    sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password'
    sudo apt-get install -y vim curl python-software-properties
    sudo apt-get update
    sudo apt-get -y install mysql-server
    sed -i "s/^bind-address/#bind-address/" /etc/mysql/my.cnf
    mysql --user=root --password=password -e "GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION; FLUSH PRIVILEGES; SET GLOBAL max_connect_errors=10000;"
    mysql --user=root --password=password -e "CREATE DATABASE tasklogs;"
    sudo /etc/init.d/mysql restart
  SHELL
  config.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777", "fmode=666"]
  config.vm.network "private_network", ip: "33.33.33.10", type: "dhcp", auto_config: false
end