# Module04 - Cloud Introduction

## Objectifs

- Préparer l'environnement de travail
- Découverte du portail Azure
- Installation du Azure CLI

## Exercice 1 - Préparation de l'environnement

### Tâche 1 - Validation du compte Azure

- Vérifier que vous avez un compte Azure
  - Connectez-vous à https://portal.azure.com
  - Sur votre cahier de laboratoire, notez le nom de votre abonnement
- Si vous n'avez pas de compte Azure, vous pouvez en créer un gratuitement (si crédit non utilisé) :
  - https://azure.microsoft.com/fr-ca/free/students/
- Pour accéder au menu étudiant à partir du portail, simplement se rendre sur le service Azure "Education".

### Tâche 2 - Installation du Azure CLI

- Installez le Azure CLI sur votre machine
  - https://docs.microsoft.com/fr-ca/cli/azure/install-azure-cli
- Testez l'installation
  - Ouvrez un terminal
  - Exécutez la commande `az login`
  - Connectez-vous avec votre compte Azure
  - Exécutez la commande `az account list`
  - Notez le nom de votre abonnement
  - Exécutez la commande `az account set --subscription "Nom de votre abonnement"`
  - Exécutez la commande `az account show`
  - Notez le nom de votre abonnement sur votre cahier de laboratoire et valider que c'est le même que celui de la tâche précédente

## Exercice 2 - Découverte du portail Azure

### Tâche 1 - Création d'une ressource par l'interface web

- Créez une ressource Azure
  - Ouvrez le portail Azure
  - Cliquez sur `Créer une ressource` (en haut à gauche)
  - Sélectionnez `Storage account` (Compte de stockage)
  - Choisissez votre abonnement, un groupe de ressources et le nom "RG-General" pour votre compte de stockage
  - Au niveau de la région, choisissez `Canada east`
  - Pour la redondance de stockage, choisissez `Stockage localement redondant` (LRS)
  - Ajoutez les étiquettes (tags) suivantes :
    - `cohorte` : `4393`
    - `session` : `A22`
    - `cours` : `420-W44-SF`
    - `module` : `M04`
  - Créez la ressource
  - Une fois téléchargé, cliquez sur le bouton `Déployer` puis `Vérifier + créer`

### Tâche 2 - Affichage du Cloud Shell

- Ouvrez le Cloud Shell
  - Cliquez sur le bouton `Cloud Shell` (en haut à droite) (Vous pouvez aussi utiliser l'URI https://shell.azure.com/)
  - Choisissez `Bash` (en haut à droite)
  - Si vous n'avez pas de Cloud Shell, cliquez sur `Créer un Cloud Shell`
    - Cliquez sur "Afficher les paramètres avancés". Autrement, un nouveau compte de stockage sera créé. Sélectionnez&nbsp;:
      - Votre bonne région
      - Votre groupe de ressources
      - Votre compte de stockage
      - Créez un partage de fichier (le nom a peu d'importance)
  - Une fois le Cloud Shell ouvert, exécutez la commande `az account show`
  - Notez le nom de votre abonnement sur votre cahier de laboratoire et valider que c'est le même que celui de la tâche précédente
- Allez dans le dossier `~/clouddrive`
- Créez le fichier `test.txt` avec le contenu suivant :
  - `Bonjour, je suis un fichier texte créé à partir du Cloud Shell`
- Retournez dans le portail :
  - Allez dans le groupe de ressources que vous aviez créé
  - Allez dans le compte de stockage
  - Allez dans `partage de fichiers`
  - Validez que vous voyez bien votre fichier
  - Téléchargez le fichier `test.txt` sur votre machine et validez que le contenu est correct

### Tâche 3 - Création d'une ressource par le Cloud Shell

- Ouvrez un terminal sur votre ordinateur
- Vérifiez que vous êtes bien connecté à votre compte Azure
  - Exécutez la commande `az account show`
  - Valider que c'est le même que celui de la tâche précédente
- Créez un nouveau compte de stockage :
  - Créez un nouveau groupe de ressources :
    - Exécutez la commande `az group create --name "M04-Ex02-T03" --location "canadaeast" --tags "cohorte=4393" "session=A22" "cours=420-W44-SF" "module=M04"`
    - Validez le résultat de la commande avec la commande `az group list`
  - Créez un nouveau compte de stockage :
    - Exécutez la commande `az storage account create --name "m04exercice2t03" --location "canadaeast" --resource-group "M04-Ex02-T03" --sku "Standard_LRS"`
    - Validez le résultat de la commande avec la commande `az storage account list`

## Exercice 3 - Nettoyage des ressources

### Tâche 1 - Suppression des ressources par le portail

Supprimez les ressources créées dans l'exercice 2 / tâche 1 :

- À partir du portail, allez dans le groupe de ressources que vous aviez créé
- Supprimez le groupe de ressources
- Validez que le groupe de ressources a bien été supprimé

### Tâche 2 - Suppression des ressources par le Azure CLI

Supprimez les ressources créées dans l'exercice 2 / tâche 3 :

- Ouvrez un terminal sur votre ordinateur
- Liste les groupes de ressources :
  - Exécutez la commande `az group list`
- Supprimer le groupe de ressources :
  - Exécutez la commande `az group delete --name "M04-Ex02-T03"`
- Validez que le groupe de ressources a bien été supprimé
  - Exécutez la commande `az group list`

## Exercice 4 - Création d'une VM Linux

Le but de cet exercice est de créer une VM Linux avec le port 80 ouvert. La première partie de l'exercice est à faire dans le portail Azure, la seconde partie est à faire avec le Azure CLI.

### Tâche 1 - Création d'une VM Linux dans le portail Azure

À l'aide du portail Azure, créez une VM Linux avec le port 80 ouvert :

- Créez le groupe de ressources "M04-Ex04-T01" dans la région "Canada East"
- Créez une machine virtuelle à l'aide du menu "machine virtuelle" à partir du menu des services
- Choisissez votre abonnement, le groupe de ressources et le nom "M04-Ex04-T01" pour votre machine virtuelle
- Choisissez la région "Canada East"
- !!!Choisissez la taille de la machine virtuelle "Standard B1ls" qui est la plus petite machine virtuelle Linux!!!
- Choisissez une image Linux de type Ubuntu Server 18.04 LTS ou supérieure
- Choisissez un nom d'utilisateur et un mot de passe
- Autorisez le port 80 et le port 22
- Dans l'onglet "Mis en réseau", vérifiez que vous avez bien une adresse IP publique qui sera créée
- Dans l'onglet "Administration", cochez l'option "Activer l'arrêt automatique". Laissez l'heure par défaut et modifiez le fuseau horaire à "(UTC-05:00) Eastern Time (US & Canada)"
- Ajoutez les étiquettes (tags) suivantes :
  - `cohorte` : `4393`
  - `session` : `A22`
  - `cours` : `420-W44-SF`
  - `module` : `M04`
- Cliquez sur "Valider et créer" puis sur "Créer" (Si vous avez des erreurs corrigez les et recommencez)
- Connectez-vous à votre machine virtuelle en SSH à l'aide de l'adresse IP publique (ouvrez la ressource dans le portail Azure pour y accéder) et du nom d'utilisateur et du mot de passe que vous avez choisi
- Sur votre machine virtuelle, exécutez la commande `sudo apt -y update` puis `sudo apt -y upgrade`
- Installez le proxy Nginx avec la commande `sudo apt -y install nginx`
- Éditez le fichier utilisé par défaut par Nginx (sur ma machine : "/var/www/html/index.nginx-debian.html") avec la commande `sudo nano <nom du fichier>` ou `sudo vi <nom du fichier>` et écrivez un message que vous devriez reconnaître.
- À l'aide de votre navigateur, accédez à l'adresse IP publique de votre machine virtuelle et validez que vous voyez le message que vous avez écrit
- Effacez votre groupe de ressources "M04-Ex04-T01" avec tout ce que vous avez dedans pour ne pas gaspiller d'argent

### Tâche 2 - Création d'une VM Linux avec le Azure CLI

À l'aide du Azure CLI, créez une VM Linux avec le port 80 ouvert :

- Ouvrez un terminal sur votre ordinateur
- Vérifiez que vous êtes bien connecté à votre compte Azure
  - Exécutez la commande `az account show`
  - Valider que c'est le même que celui de la tâche précédente

- Créez un nouveau groupe de ressources. Utilisez la commande précédente pour créer un nouveau groupe de ressources nommé "M04-Ex04-T02"
- Listez les images disponibles. Utilisez la commande `az vm image list` pour lister les images disponibles
- Listez versions disponibles pour l'image Ubuntu en utilisant la commande `az vm image list-skus --publisher "Canonical" --offer "UbuntuServer" --location "canadaeast"`
- Dans le résultat, recherchez la version 18.04-LTS et notez le nom de la version
- Listez les tailles de VM disponibles. Utilisez la commande `az vm list-sizes --location canadaeast` pour lister les tailles de VM disponibles
- Comme vous le voyez, il y a beaucoup de taille de VM. Pour cette tâche, nous allons utiliser la taille "Standard_B1ls" qui est la plus petite taille de VM Linux
- Créez la VM avec la commande `az vm create --resource-group "M04-Ex04-T02" --name "M04-Ex04-T02-VM" --image "UbuntuLTS" --size "Standard_B1ls" --admin-username "adminuser" --admin-password "Password123.." --public-ip-sku Basic --location "canadaeast" --tags "cohorte=4393" "session=A22" "cours=420-W44-SF" "module=M04"` (Si vous utilisez un autre groupe de ressources, n'oubliez pas de le changer dans la commande)
- Listez les machines virtuelles pour vérifier que votre VM a bien été créée avec la commande `az vm list`
- Installez Ngnix grâce à la commande suivante : `az vm run-command invoke --resource-group "M04-Ex04-T02" --name "M04-Ex04-T02-VM" --command-id RunShellScript --scripts "sudo apt -y update && sudo apt -y upgrade && sudo apt -y install nginx"`
- Ouvrez le port 80 avec la commande suivante : `az vm open-port --resource-group "M04-Ex04-T02" --name "M04-Ex04-T02-VM" --port 80` si cela ne fonctionne pas allez dans le portail Azure et validez la configuration
- Récupérez l'adresse IP publique de votre VM avec la commande `az vm list-ip-addresses --resource-group "M04-Ex04-T02" --name "M04-Ex04-T02-VM"`
- Connectez-vous à votre site web à l'aide de votre navigateur et vérifiez que vous voyez le message par défaut de Nginx
- Connectez sur votre VM en SSH avec la commande `ssh adminuser@<adresse IP publique de votre VM>` et modifiez le fichier par défaut de Nginx avec la commande `sudo nano /var/www/html/index.nginx-debian.html` ou `sudo vi /var/www/html/index.nginx-debian.html` et écrivez un message que vous devriez reconnaître.
- Validez que le site est bien modifié
- Supprimer le groupe de ressources "M04-Ex04-T02" avec tout ce que vous avez dedans pour ne pas gaspiller d'argent avec la commande `az group delete --name "M04-Ex04-T02" --yes`

<details>
    <summary>Triche #1 - Création d'un groupe de ressources Exercice 4 / Tâche 2 :</summary>

```bash
az group create --name M04-Ex04-T02 --location canadaeast --tags "cohorte=4393" "session=A22" "cours=420-W44-SF" "module=M04"
```

</details>

### Tâche 3 - Création d'une VM Linux à partir d'un template ARM

- Débutez la création de la VM Linux "M04-Ex04-T03-VM" à partir du portail Azure. Au lieu de créer la ressource, téléchargez le template ARM de la VM
- Positionnez-vous dans le répertoire de votre choix et désarchiver le fichier téléchargé
- Modifiez le fichier `parameters.json` pour définir le mot de passe du compte administrateur (vers la fin du document JSON)
- En ligne de commande, créez le groupe de ressources `M04-Ex04-T03`
- Pour exécuter le déploiement, utilisez la commande `az deployment group create --resource-group M04-Ex04-T03 --template-file template.json --parameters @parameters.json`
- Installez Ngnix et ouvrez le port 80 avec les mêmes commandes que dans la tâche précédente mais en remplaçant le nom de la VM et celui du groupe de ressources
- Validez que le tout fonctionne (Si le port n'est pas ouvert, l'ouvrir !)
- Supprimer le groupe de ressources "M04-Ex04-T03" avec tout ce que vous avez dedans pour ne pas gaspiller d'argent avec la commande `az group delete --name "M04-Ex04-T03" --yes`

Fini !