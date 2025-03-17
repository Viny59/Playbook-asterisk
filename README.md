# Configuration et exécution d'un Playbook Ansible pour Asterisk

## 1. Configuration de la connexion SSH entre la machine Ansible et le serveur distant
Avant d'exécuter le playbook Ansible, il est nécessaire de configurer une connexion SSH entre la machine de contrôle Ansible et le serveur distant.

### 1.1 Générer une clé SSH sur la machine Ansible
Exécutez la commande suivante pour générer une paire de clés SSH :
```bash
ssh-keygen
```
Appuyez sur **Entrée** pour accepter l’emplacement par défaut et laissez le champ de passphrase vide si vous souhaitez une connexion sans mot de passe.

### 1.2 Copier la clé SSH vers le serveur distant
Utilisez la commande suivante pour copier la clé publique sur le serveur distant :
```bash
ssh-copy-id admin@{IP_DU_SERVEUR}
```
Remplacez `{IP_DU_SERVEUR}` par l’adresse IP de votre serveur cible. Une fois cette étape réalisée, vous devriez pouvoir vous connecter sans mot de passe avec la commande :
```bash
ssh admin@{IP_DU_SERVEUR}
```

## 2. Création des fichiers nécessaires

### 2.1 Création du fichier `asterisk.yml`
Créez un fichier nommé `asterisk.yml`, qui contiendra le playbook Ansible pour l'installation et la mise à jour d'Asterisk.

### 2.2 Création du fichier `inventory.ini`
Créez un fichier `inventory.ini` pour définir la liste des serveurs cibles. Exemple de configuration :
```ini
[asterisk_servers]
{IP_DU_SERVEUR} ansible_user=admin
```
Remplacez `{IP_DU_SERVEUR}` par l’adresse IP de votre serveur Asterisk.

## 3. Exécution du Playbook Ansible

Pour exécuter le playbook et installer ou mettre à jour Asterisk, utilisez la commande suivante :
```bash
ansible-playbook -i inventory.ini asterisk.yml
```
Cela exécutera le playbook sur le serveur défini dans `inventory.ini`.

## 4. Vérification de l'installation d'Asterisk
Une fois le playbook terminé, connectez-vous à votre serveur et exécutez la commande suivante pour vérifier le bon fonctionnement d'Asterisk :
```bash
asterisk -vvvvc
```
