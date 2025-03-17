# Ansible Playbook pour Déploiement Asterisk

Ce playbook Ansible automatise l'installation et la configuration d'Asterisk.

## Description

Le playbook installe Asterisk, incluant les dépendances et la configuration de base.

## Prérequis

*   Ansible installé.
*   Accès SSH avec sudo.
*   Connexion Internet.

## Inventaire

Configurez votre fichier `inventory` avec l'ip du serveur cible.

## Utilisation

1.  **Créez le fichier du playbook (si nécessaire) :** Si vous n'avez pas déjà le fichier `asterisk_playbook.yml`, créez-le avec `nano`  :

    ```
    nano asterisk_playbook.yml
    ```

    Copiez-collez le contenu du playbook dans ce fichier et enregistrez-le.

3.  **Modifiez l'inventaire :** Assurez-vous que le fichier `inventory` contient les informations correctes pour votre serveur cible.

4.  **Exécutez le playbook :**

    ```
    ansible-playbook -i inventory asterisk_playbook.yml
    ```


    Après l'exécution du playbook, connectez-vous a la machine cible via SSH et exécutez :

        ```
        asterisk -vvvvc
        ```

        
