# vagrant_nodejs
Vagrant Development Environment for Nodejs projects (Mysql + Mongodb support)

# How it works

This vagrant developement environment is multi-machine.

* A machine for nodejs
* A machine for mysql
* A machine for Mongodb

You can choose to work with one or all of them.

```
git clone https://github.com/eon01/vagrant_nodejs.git
cd vagrant_nodejs

#Choose what do you want to work with by executing 'up' on the appropriate machine
vagrant up nodejs
vagrant up mysql
vagrant up mongodb

#Start provisionning your selected machine
vagrant reload --provision-with shell,salt nodejs
vagrant reload --provision-with shell,salt mysql
vagrant reload --provision-with shell,salt mongodb

#If everything is ok, you can ssh to your machine
vagrant ssh nodejs
vagrant ssh mysql
vagrant ssh mongodb

```
# Hosts and Network

The configuration is :
(see forwarded ports and local ip to communicate between your instances)

```
nodejs
    nodejs.vm.network "forwarded_port", guest: 80, host: 8001
    nodejs.vm.network  "forwarded_port", guest: 3600, host: 8002
    nodejs.vm.network "private_network", ip: "10.0.0.10"

mysql
    mysql.vm.network "forwarded_port", guest: 3306, host: 8003
    mysql.vm.network "private_network", ip: "10.0.0.11"

mongodb
    mongodb.vm.network "forwarded_port", guest: 27017, host: 8004
    mongodb.vm.network "private_network", ip: "10.0.0.12"
```
