# README - Projet éducatif Ansible & Docker : Déploiement MediaWiki

Ce projet a pour but d'apprendre à automatiser le déploiement d'une application web (MediaWiki) avec Ansible et Docker. Il est conçu pour découvrir les bases de l'infrastructure as code, la modularité et la sécurité des mots de passe.

## Structure du projet

- **ansible.cfg** : Configuration d'Ansible (chemin inventaire, options globales).
- **docker-compose.yml** : Définit les conteneurs Docker simulant les serveurs :
  - `http1` : serveur web (Apache/PHP)
  - `bdd1` : serveur base de données (MariaDB)
- **hosts.ini** : Inventaire Ansible, liste les hôtes cibles et leurs paramètres de connexion.
- **install-apache.yml** : Playbook pour installer et configurer Apache.
- **install-mariadb.yml** : Playbook pour installer et configurer MariaDB.
- **install-mediawiki.yml** : Playbook pour installer MediaWiki.
- **roles/** : Dossier contenant les rôles Ansible pour chaque service :
  - `apache/` : Installation et configuration d'Apache et PHP.
  - `mariadb/` : Installation et configuration de MariaDB.
  - `mediawiki/` : Installation et configuration de MediaWiki (sous-rôles pour Apache et DB).

## Définitions des notions Ansible

- **Inventaire** : Fichier listant les hôtes sur lesquels Ansible agit (ex : `hosts.ini`).
- **Playbook** : Fichier YAML décrivant une suite de tâches à exécuter sur les hôtes.
- **Rôle** : Structure modulaire regroupant tâches, variables, templates et handlers pour une fonctionnalité précise.
- **Task (tâche)** : Action individuelle exécutée par Ansible (ex : installer un paquet).
- **Handler** : Action déclenchée par une notification (ex : redémarrer Apache).
- **Module** : Composant Ansible réalisant une tâche spécifique (ex : gestion MySQL).
- **Variable** : Valeur dynamique utilisée pour personnaliser l'exécution.
- **Template** : Fichier de configuration dynamique utilisant Jinja2.
- **Vault** : Système de chiffrement d'Ansible pour sécuriser les secrets.

## Fonctionnement

1. **Lancer les serveurs Docker**
   ```bash
   docker-compose up -d
   ```
2. **Vérifier la connexion Ansible**
   ```bash
   ansible -i hosts.ini all -m ping
   ```
3. **Déployer les services**
   - Apache : `ansible-playbook -i hosts.ini install-apache.yml`
   - MariaDB : `ansible-playbook -i hosts.ini install-mariadb.yml`
   - MediaWiki : `ansible-playbook -i hosts.ini install-mediawiki.yml`

## Points pédagogiques

- Comprendre la structure d'un projet Ansible modulaire.
- Utiliser Ansible Vault pour sécuriser les mots de passe.
- Automatiser le déploiement d'applications web.
- Utiliser Docker pour simuler une infrastructure multi-serveurs.

## Conseils

- Vérifiez la cohérence des noms d'hôtes entre `docker-compose.yml` et `hosts.ini`.
- Adaptez les rôles pour installer les bons paquets sur chaque serveur.
- Utilisez Ansible Vault pour tous les secrets.
- Modifiez les playbooks pour personnaliser votre installation MediaWiki.

---

Explorez chaque rôle et chaque playbook pour comprendre leur fonctionnement et les adapter à vos besoins !

