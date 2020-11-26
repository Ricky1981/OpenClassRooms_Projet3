# Projet 03 - Créez votre environnement de travail local

Le but de cette documentation est de définir les prérequis necessaires a l'utilisation du Vagrantfile de ce repository ainsi que de fournir une explication des différentes parties composants ce fichier.
La machine virtuelle obtenue sera une debian 10 et disposera d'une IP fixe à savoir 192.168.33.10.
Bien vérifier préalablement que votre réseau n'utilise pas cette IP.

## Prérequis

- [Git](https://git-scm.com/book/fr/v2/D%C3%A9marrage-rapide-Installation-de-Git) ~> 2.20
- [Vagrant](https://www.vagrantup.com/docs/installation) ~> 2.2.6
- Plugin scp de vagrant : `vagrant plugin install vagrant-scp` 
- [VirtualBox ainsi que son pack d'extension](https://www.virtualbox.org/wiki/Downloads) ~> 6.1.16
- Disposer de l’image vagrant `vagrant-debian10.6.0` et la placer dans le meme repertoire où la commande `vagrant up` sera exécutée 

## Configuration SSH

Vagrant se connecte parfaitement via la commande `vagrant ssh`. 
Cependant, si vous souhaitez utiliser la commande `ssh [user]@[IP]`, il faudra ajouter des informations dans le fichier ~/.ssh/config.
Ci-dessous les étapes à respecter : 
1°/ Nous consultons la configuration ssh de vagrant via la commande `vagrant ssh-config` :

```hcl
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/seb/.vagrant.d/insecure_private_key
  IdentitiesOnly yes
  LogLevel FATAL`
```

2°/ Vagrant nous affiche alors la configuration qu'il utilise. Comme on connait l'adresse IP de la machine et le chemin vers sa clé privée, on peut se rendre dans le fichier `~/.ssh/config` pour ajouter une configuration :

```hcl
Host 192.168.33.10
  User vagrant
  Port 22
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/seb/.vagrant.d/insecure_private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

 La configuration sera ainsi utilisée avec la bonne clé privée et la connexion peut être établie via la commande `ssh [user]@[IP]`


