# Ansible Docker - Exercice de Formation

Ce projet est un exercice de formation qui démontre l'utilisation d'Ansible avec Vagrant pour automatiser le déploiement de Docker et de services dans un environnement virtualisé.

## Description

Ce projet configure automatiquement un environnement composé de :
- Une machine **master** (serveur Ansible)
- Une ou plusieurs machines **slave** (cibles de déploiement)

L'objectif est d'installer Docker sur les machines slaves et de déployer des services (PostgreSQL, Prometheus) via des playbooks Ansible.

## Prérequis

- [Vagrant](https://www.vagrantup.com/) installé
- [VMware Desktop](https://www.vmware.com/products/workstation-pro.html) ou VirtualBox
- Au moins 3 GB de RAM disponible

## Structure du Projet

```
ansible_docker/
├── vagrantfile              # Configuration Vagrant
├── ansible/
│   ├── ansible.cfg         # Configuration Ansible
│   ├── hosts               # Inventaire des machines
│   ├── playbooks/
│   │   ├── install_docker.yml    # Installation de Docker
│   │   ├── deploy_services.yml   # Déploiement des services
│   │   └── vault.yml             # Variables chiffrées
│   └── roles/              # Rôles Ansible
```

## Configuration

Le Vagrantfile est configuré avec les paramètres suivants :
- **Image** : Ubuntu 22.04 LTS
- **Master** : 1024 MB RAM, IP 192.168.10.10
- **Slave(s)** : 2048 MB RAM, IP 192.168.10.11+
- **Réseau** : Réseau privé 192.168.10.x

## Utilisation

### 1. Démarrage de l'environnement

```bash
vagrant up
```

Cette commande va :
- Créer et configurer les machines virtuelles
- Installer Ansible sur la machine master
- Configurer l'authentification SSH entre master et slaves
- Exécuter automatiquement les playbooks

### 2. Connexion à la machine master

```bash
vagrant ssh master
```

### 3. Vérification du déploiement

Une fois connecté au master, vous pouvez :
- Vérifier l'inventaire : `ansible all --list-hosts`
- Tester la connectivité : `ansible all -m ping`
- Voir l'arborescence : `tree ansible-docker/`

## Playbooks Disponibles

### install_docker.yml
Installe Docker sur les machines du groupe `docker`.

### deploy_services.yml
Déploie PostgreSQL et Prometheus via des conteneurs Docker.

## Commandes Utiles

```bash
# Arrêter l'environnement
vagrant halt

# Redémarrer
vagrant reload

# Supprimer l'environnement
vagrant destroy

# Voir le statut des machines
vagrant status
```

## Notes de Formation

Ce projet illustre :
- Configuration d'un environnement multi-machine avec Vagrant
- Automatisation SSH et configuration réseau
- Utilisation d'Ansible pour la gestion de configuration
- Déploiement de services avec Docker
- Utilisation d'Ansible Vault pour les secrets