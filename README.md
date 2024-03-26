# TP Azure - 1 - Mémoire 5ème année

# Sujet

Dans ce TP, nous allons voir comment créer une machine virtuelle et nous verrons comment s'y connecter en RDP.
L'objectif est de pouvoir se connecter à sa VM en sécurisant son accès.

# Étape 1 : Prérequis

- Posséder un compte Azure https://portal.azure.com

# Étape 2 : Créer un abonnement

- Créer un abonnement. Lorsque vous êtes étudiant, vous pouvez bénéficier de l’offre gratuite disponible ici : https://portal.azure.com/#view/Microsoft_Azure_Education/EducationMenuBlade/~/overview

# Étape 3 : Créer un groupe de ressource

Le groupe de ressource permet de regrouper dans un projet les ressources nécessaires. Cela vous permettra de supprimer en deux cliques l'ensemble du projet pour éviter de payer inutilement.
Rendez-vous ici : https://portal.azure.com/#view/HubsExtension/BrowseResourceGroups

Vous pouvez le nommer "TP_Azure_1"

![Groupe de ressource](https://acenox.fr/memoire/gdr.png)

# Étape 4 : Créer un réseau virtuel

Onglet : Information de base 

- Nom du réseau : vnet-1
- Région : France
- Cliquer sur "Suivant"

![Vnet](https://acenox.fr/memoire/vnet1.png)

Onglet : Sécurité

- Cocher la case "Chiffrement du réseau virtuel"
- Cliquer sur "Suivant"

![Vnet 2](https://acenox.fr/memoire/vnet2.png)

Onglet : Adresse IP

- Modifier le sous réseau se nommant "défaut"
- Changer le nom du sous réseau par "subnet-1"
- Enregistrer
- Cliquer sur "vérifier + créer" puis "créer"

![Vnet 3](https://acenox.fr/memoire/vnet3.png)

# Étape 5 : Créer un groupe de sécurité d'application

L'objectif est de regrouper des serveurs dont les fonctions sont similaires.

- Nom : asg-tp
- Région : France
- Cliquer sur "vérifier + créer" puis "créer"

![asg1](https://acenox.fr/memoire/asg1.png)

# Étape 5 : Créer un groupe de sécurité réseau

Le groupe de sécurité réseau permet de sécuriser le trafic dans le réseau virtuel.

- Nom : nsg-1
- Région : France
- Cliquer sur "vérifier + créer" puis "créer"

# Étape 6 : Associer le groupe de sécurité au sous-réseau

- Se rendre https://portal.azure.com/#view/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2FNetworkSecurityGroups (dans groupe de sécurité réseau)
- Sélectionner nsg-1 (s'il n'apparaît pas, vous pouvez rafraichir la page).
- Sélectionner "Sous-réseaux"

![asg2](https://acenox.fr/memoire/asg2.png)

- Sélectionner votre réseau virtuel (nom de votre ressource)
- En sous-réseau y ajouter : subnet-1
- Cliquer sur "OK" pour enregistrer vos modifications

![asg3](https://acenox.fr/memoire/asg3.png)

# Étape 7 : Créer des règles de sécurité

- Se rendre dans l'onglet "Règles de sécurité de trafic entrant"
- Cliquer sur "Ajouter"
- Sélectionner le groupe de sécurité "asg-tp"
- Service : RDP
- Nom : allow-rdp
- Cliquer sur "Ajouter"

![rdp](https://acenox.fr/memoire/rdp.png)

# Étape 8 : Créer une machine virtuelle

- Cliquer sur "Créer une machine virtuelle Azure"
- Nom : VM-1
- Région : France
- Zone de disponibilité : Acuune redondance d'infrastructure requise
- Type de sécurité : Standard
- Image : Windows Server 2022 Datacenter - x64 Gen2
- Taille : Garder par défaut
- Nom d'utilisateur : esgi
- Mot de passe : Définissez un mot de passe
- Port d'entrée : Sélectionner "Aucun"
- Cliquer sur "Suivant : Disques" puis "Suivant : Réseaux"

- Réseau Virtuel : vnet-1
- Sous réseau : subnet-1 (10.0.0.0/24)
- Garder le reste par défaut
- Cliquer sur "vérifier + créer" puis "créer"

# Étape 9 : Configuration de la machine virtuelle

- Cliquer sur votre machine virtuelle "VM-1"
- Se rendre dans l'onglet "Groupe de sécurité d'application"
- Cliquer sur "+ Groupes de sécurité d'application"
- Sélectionner votre groupe "asg-tp"
- Cliquer sur "Ajouter"

![vm](https://acenox.fr/memoire/vm1.png)

# Étape 10 : Tester la connexion

- Se rendre dans l'onglet "Connexion"
- Cliquer sur "Télécharger un fichier RDP"
- Puis ouvrez le fichier & renseinez-y vos identifiants de connexion

Félicitations ! Vous avez terminé ce premier TP 🥳​ Vous avez su déployer une machine virtuelle et vous y connecter à distance.
Pour aller plus loin, il est recommandé d'utiliser Azure Bastion pour sécuriser la connexion. De plus, grâce à ce système votre VM n'aura plus besoin d'avoir obligatoirement une IP publique ou d'agent installé pour s'y connecter.
