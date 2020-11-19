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
  config.vm.box = "vagrant-debian10.6.0"
  #config.vm.box_url = "file:///home/seb/Documents/ownCloud/OpenClassRoom/Projet_03_RYKALA_Sebastien/vagrantBox/vagrant-debian10.6.0.box"
 
  # Ajout d'une valeur d'un timeout plus bas que par défaut pour rendre les tests plus rapide
  #config.vm.boot_timeout = 40
 
  # Configuration SSH
  #config.ssh.private_key_path = "~/.ssh/id_rsa"
  #config.ssh.forward_agent = true
  config.ssh.insert_key = false
  # https://medium.com/@Sohjiro/add-public-key-to-vagrant-4bd5424521bf
  #config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
  #config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
  
  #config.vm.provision "shell", inline: <<-EOC
  #  sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
  #  sudo systemctl restart sshd.service
  #  echo "finished"
  #EOC

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

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
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
	## Ajout clé SSH public de l'utilisateur qui souhaite utiliser la VM Vagrant
	#cat ~/.ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys	

	# Ajout Editeur Texte     
	apt-get update
     	#apt-get install -y apache2
     	apt-get install -y vim

     	# Ajout depot Ansible"
     	DEPOTFILE='/etc/apt/sources.list'
	LINETOADD_ANSIBLE='deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main'
     	#https://linux.die.net/man/1/grep --> ici la ligne ne s'ajoutera que si celle ci n'est pas déjà présente dans sources.list
     	grep -qFx "$LINETOADD_ANSIBLE" "$DEPOTFILE" || echo "$LINETOADD_ANSIBLE" >> "$DEPOTFILE"
     	#echo 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' >> /etc/apt/sources.list
     	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
     	apt-get update
     	apt-get install -y ansible

   SHELL
end
