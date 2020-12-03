# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
   # Utilisation de la boxe que nous avons choisi d'utiliser 
   config.vm.box = "generic/debian10"
   # Dans le cas d'une construction d'image personnel, le paramètre config.vm.box_url est à utiliser si vous souhaitez mettre l'image ailleurs que dans le repertoire courant
   # config.vm.box_url = "file:///home/seb/Documents/ownCloud/OpenClassRoom/Projet_03_RYKALA_Sebastien/vagrantBox/vagrant-debian10.6.0.box"
 
   # Le paramètre config.vm.boot_timeout permet de changer la valeur du timeout (défaut 300 secondes) pour rendre les tests plus rapide en cas de problème
   # config.vm.boot_timeout = 40
 
   # Configuration SSH
   # Nous mettons le paramètre config.ssh.insert_key à false pour que Vagrant n'ajoute pas une clé de façon automatique (par défaut à true)
   config.ssh.insert_key = false
  
   # Nous créons un réseau privé pour permettre à notre machine de trouver et pouvoir communiquer avec notre VM 
   config.vm.network "private_network", ip: "192.168.33.10"
    
   # Nous personnalisons notre VM en fixant la mémoire et en attribuant un nom à notre machine virtuelle
   config.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
      vb.name = "Projet 03 - Creez votre environnement de travail local"
   end

   # Décommenter ces 3 lignes après le premier lancement afin de gagner du temps lors de la vérification des "Guest Additions".
   # Etant donné que le plugin vbguest a été ajouté lors du premier lancement, nous pouvons indiquer à vagrant de ne pas tenter l'update 
   #if Vagrant.has_plugin?("vagrant-vbguest")
   #   config.vbguest.auto_update = false  
   #end
  
   # Nous provisionnons notre VM avec les outils dont nous avons besoin pour travailler
   config.vm.provision "shell", inline: <<-SHELL
	
	   # Ajout Editeur Texte     
	   apt-get update
     	apt-get install -y vim

     	# Ajout depot Ansible"
     	DEPOTFILE='/etc/apt/sources.list'
	   LINETOADD_ANSIBLE='deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main'
     	# ici la ligne ne s'ajoutera que si celle ci n'est pas déjà présente dans sources.list
     	grep -qFx "$LINETOADD_ANSIBLE" "$DEPOTFILE" || echo "$LINETOADD_ANSIBLE" >> "$DEPOTFILE"
     	apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
     	apt-get update
     	apt-get install -y ansible

	   # Ajout Docker
	   apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
	   curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
	   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
	   sudo apt-get update
	   sudo apt-get install -y docker-ce docker-ce-cli containerd.io
	   usermod -aG docker vagrant	

   SHELL
end