# Projet 03 - Créez votre environnement de travail local

Le but de cette documentation est de définir les prérequis necessaires a l'utilisation du Vagrantfile de ce repository ainsi que de fournir une explication des différentes parties composants ce fichier.
La machine virtuelle obtenue sera une debian 10 et disposera d'une IP fixe à savoir 192.168.33.10.
Bien vérifier préalablement que votre réseau n'utilise pas cette IP.

A titre informatif, plus de détail concernant l'image vagrant utilisée [ici](https://app.vagrantup.com/generic/boxes/debian10)

## Prérequis

- [Git](https://git-scm.com/book/fr/v2/D%C3%A9marrage-rapide-Installation-de-Git) ~> 2.20
- [Vagrant](https://www.vagrantup.com/docs/installation) ~> 2.2.6
- Plugin scp de vagrant : `vagrant plugin install vagrant-scp` 
- Plugin vbguest de vagrant : `vagrant plugin install vagrant-vbguest`
- [VirtualBox ainsi que son pack d'extension](https://www.virtualbox.org/wiki/Downloads) ~> 6.1.16

## Installation de la machine virtuelle "vierge"

1. Créer un repertoire sur poste, par exemple "vagrant" : `mkdir ~/vagrant`
2. Se déplacer dans le répertoire "vagrant" : `cd ~/vagrant`
3. Récupérer la dernière version du repository en lançant la commande suivante : `git clone --depth 1 https://github.com/Ricky1981/OpenClassRooms_Projet3_Vagrant.git .`
4. Lancer la construction via la commande `vagrant up`
5. Après un certain temps, la machine virtuelle est créée et il vous est possible de prendre la main à distance en ssh via la commande `vagrant ssh` (si vous souhaitez une autre méthode de connection, merci de consulter la section [suivante](#ssh))

## Test des différents outils sur la machine virtuelle

Les composants du tableaux ci-dessous sont les composants qui ont été ajouté dans le Vagrantfile et ne proviennent donc pas de l'image par défaut.
Toutes les commandes ci-dessous sont à faire une fois la connection SSH sur l'hôte distant est opérationnel :

| Composant | Commande | Retour |
|-----------|----------|--------|
| Editeur de texte | `vim --version` | VIM - Vi IMproved 8.1 |
| Ansible | `ansible --version` | ansible 2.9.15 |
| Docker | `docker --version` | Docker version 19.03.14 |



## <a name="ssh"></a> Configuration SSH

Ce paragraphe vous propose de configurer SSH sur votre poste afin d'utiliser la façon commune à l'utilisation de la commande ssh.
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


