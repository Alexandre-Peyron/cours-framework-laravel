# Installation de HomeStead

Premier réflexe : la [documentation](https://laravel.com/docs/5.6/homestead) 

> Cette partie là est optionnelle. Si vous ne souhaitez pas utiliser Homestead, installez un projet Laravel de manière classique sur votre environnement de travail et passez à la suite.

Laravel fournit tout un environnement de développement local.

Il s'agit d'une machine virtuelle contenant déjà tous les outils nécessaires 
pour le développement d'un projet Laravel.

Par exemple :
- Git
- Différentes versions de PHP
- Composer
- Différents SGBD
- Redis
- Memcached
- ...

### Vagrant

Ma machine virtuelle est basé sur [vagrant](https://www.vagrantup.com/).

Installez-le.


### Machine Virtuelle

Dans un second temps, installez un système de machine virtuelle (au choix).

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads) - Gratuit
- [https://www.vmware.com/](https://www.vmware.com/)
- [Parallels](https://www.parallels.com/products/desktop/) - Payant
- [Hyper V](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) - Gratuit - Microsoft

Je vous conseille VirtualBox qui est gratuit et multi OS.

### Box

Lancez la commande suivante :

```bash
vagrant box add laravel/homestead
```

Patientez.

### Configuration

Pour la suite, la documentation explique très bien les étapes à suivre :

- Relier votre dossier de code local à celui de la machine virutelle
- Créer le virtual host avec Nginx
- Installer de configurer le SGBD
- Se connecter en SSH
- Sauvegarde de la BDD
- Envoi d'email