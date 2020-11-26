# Projet 03 - Créez votre environnement de travail local

Le but de cette documentation est de définir les prérequis necessaires a l'utilisation du Vagrantfile de ce repository ainsi que de fournir une explication des différentes parties composants ce fichier.
La machine virtuelle obtenue sera une debian 10

## Prérequis

- [Git](https://git-scm.com/book/fr/v2/D%C3%A9marrage-rapide-Installation-de-Git) ~> 2.20
- [Vagrant](https://www.vagrantup.com/docs/installation) ~> 2.2.6
- Plugin scp de vagrant : `vagrant plugin install vagrant-scp` 
- [VirtualBox ainsi que son pack d'extension](https://www.virtualbox.org/wiki/Downloads) ~> 6.1.16
- Disposer de l’image vagrant `vagrant-debian10.6.0` et la placer dans le meme repertoire où la commande `vagrant up` sera exécutée 

