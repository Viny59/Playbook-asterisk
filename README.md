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
serveur_asterisk ansible_host={IP_DU_SERVEUR} ansible_user=admin ansible_ssh_private_key_file=~/.ssh/id_rsa
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
Cette commande permet d’ouvrir la console Asterisk en mode interactif avec un niveau de verbosité élevé.

## 5. Vérification de la version d'Asterisk
Pour vérifier la version d'Asterisk installée, utilisez l'une des commandes suivantes :

### 5.1 En ligne de commande
```bash
asterisk -V
```
Cela affichera une sortie similaire à :
```
Asterisk 18.12.1
```

### 5.2 Depuis la console Asterisk
Si Asterisk est en cours d'exécution, entrez dans la console en mode interactif avec :
```bash
asterisk -vvvvc
```
Puis, exécutez la commande suivante :
```bash
core show version
```
Cela affichera des informations détaillées sur la version d'Asterisk en cours d'exécution.

