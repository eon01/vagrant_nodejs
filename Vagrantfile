Vagrant.configure(2) do |config|
 
  config.vm.define :nodejs do |nodejs|
    nodejs.vm.box = "ubuntu/trusty64"
    nodejs.vm.hostname = "nodejs"
    nodejs.ssh.pty = true

    nodejs.vm.network "forwarded_port", guest: 80, host: 8001
    nodejs.vm.network  "forwarded_port", guest: 3600, host: 8002
    nodejs.vm.network "private_network", ip: "10.0.0.10"

    nodejs.vm.synced_folder "salt/roots/", "/srv/salt/"
    nodejs.vm.synced_folder "salt/minion.d/", "/etc/salt/minion.d/"
    nodejs.vm.synced_folder "salt/formulas/", "/srv/formulas/"

    nodejs.vm.provision :salt do |salt|
      salt.verbose = true
      salt.minion_config = "salt/minion.yml"
      salt.run_highstate = true
      salt.colorize = true
      salt.log_level = 'all'
      salt.always_install = true
      salt.colorize = true
      salt.bootstrap_options = '-F -c /tmp/ -P'
    end

    nodejs.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--memory", "2048"]
      v.customize ["modifyvm", :id, "--cpus", "2"]
    end

    nodejs.vm.provision "shell", path: "bootstrap/nodejs_bootstrap.sh"

  end

#=================================

  config.vm.define :mysql do |mysql|
    mysql.vm.box = "ubuntu/trusty64"
    mysql.vm.hostname = "mysql"
    mysql.ssh.pty = true

    mysql.vm.network "forwarded_port", guest: 3306, host: 8003
    mysql.vm.network "private_network", ip: "10.0.0.11"

    mysql.vm.synced_folder "salt/roots/", "/srv/salt/"
    mysql.vm.synced_folder "salt/minion.d/", "/etc/salt/minion.d/"
    mysql.vm.synced_folder "salt/formulas/", "/srv/formulas/"

    mysql.vm.provision :salt do |salt|
      salt.verbose = true
      salt.minion_config = "salt/minion.yml"
      salt.run_highstate = true
      salt.colorize = true
      salt.log_level = 'all'
      salt.always_install = true
      salt.colorize = true
      salt.bootstrap_options = '-F -c /tmp/ -P'
    end

    mysql.vm.provision "shell", path: "bootstrap/mysql_bootstrap.sh"
      
  end

#=================================

  config.vm.define :mongodb do |mongodb|
    mongodb.vm.box = "ubuntu/trusty64"
    mongodb.vm.hostname = "mongodb"
    mongodb.ssh.pty = true

    mongodb.vm.network "forwarded_port", guest: 27017, host: 8004
    mongodb.vm.network "private_network", ip: "10.0.0.12"

    mongodb.vm.synced_folder "salt/roots/", "/srv/salt/"
    mongodb.vm.synced_folder "salt/minion.d/", "/etc/salt/minion.d/"
    mongodb.vm.synced_folder "salt/formulas/", "/srv/formulas/"

    mongodb.vm.provision :salt do |salt|
      salt.verbose = true
      salt.minion_config = "salt/minion.yml"
      salt.run_highstate = true
      salt.colorize = true
      salt.log_level = 'all'
      salt.always_install = true
      salt.colorize = true
      salt.bootstrap_options = '-F -c /tmp/ -P'
    end

    mongodb.vm.provision "shell", path: "bootstrap/mongodb_bootstrap.sh"

  end


end

