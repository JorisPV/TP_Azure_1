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

Onglet : Sécurité

- Cocher la case "Chiffrement du réseau virtuel"
- Cliquer sur "Suivant"

![Vnet 2](https://acenox.fr/memoire/vnet2.png)

Onglet : Adresse IP

- Modifier le sous réseau se nommant "défaut"

- Nom du réseau : vnet-1
- Région : France
- Cliquer sur "Suivant"

![Vnet](https://acenox.fr/memoire/vnet1.png)
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

# Étape 6 : Créer un groupe de sécurité réseau

Le groupe de sécurité réseau permet de sécuriser le trafic dans le réseau virtuel.

- Nom : nsg-1
- Région : France
- Cliquer sur "vérifier + créer" puis "créer"

![nsg1](https://acenox.fr/memoire/nsg1.png)

# Étape 7 : Associer le groupe de sécurité au sous-réseau

- Se rendre https://portal.azure.com/#view/HubsExtension/BrowseResource/resourceType/Microsoft.Network%2FNetworkSecurityGroups (dans groupe de sécurité réseau)
- Sélectionner nsg-1 (s'il n'apparaît pas, vous pouvez rafraichir la page).
- Sélectionner "Sous-réseaux"

![asg2](https://acenox.fr/memoire/asg2.png)

- Sélectionner votre réseau virtuel (nom de votre ressource)
- En sous-réseau y ajouter : subnet-1
- Cliquer sur "OK" pour enregistrer vos modifications

![asg3](https://acenox.fr/memoire/asg3.png)

# Étape 8 : Créer des règles de sécurité

- Se rendre dans l'onglet "Règles de sécurité de trafic entrant"
- Cliquer sur "Ajouter"
- Sélectionner le groupe de sécurité "asg-tp"
- Service : RDP
- Nom : allow-rdp
- Cliquer sur "Ajouter"

![rdp](https://acenox.fr/memoire/rdp.png)

# Étape 9 : Créer une machine virtuelle

- Cliquer sur "Créer une machine virtuelle Azure"
- Nom : VM-1
- Région : France
- Zone de disponibilité : Acuune redondance d'infrastructure requise
- Type de sécurité : Standard
- Image : Windows Server 2022 Datacenter - x64 Gen2
- Taille : Augmenter à B2s (b1s est insuffisant pour faire tourner Windows Server)
- Nom d'utilisateur : esgi
- Mot de passe : Définissez un mot de passe
- Port d'entrée : Sélectionner "Aucun"

![vm 3](https://acenox.fr/memoire/vm3.png)

- Cliquer sur "Suivant : Disques" puis "Suivant : Réseaux"

- Réseau Virtuel : vnet-1
- Sous réseau : subnet-1 (10.0.0.0/24)
- Garder le reste par défaut
- Cliquer sur "vérifier + créer" puis "créer"

![vm 4](https://acenox.fr/memoire/vm4.png)

# Étape 10 : Configuration de la machine virtuelle

- Cliquer sur votre machine virtuelle "VM-1"
- Se rendre dans l'onglet "Groupe de sécurité d'application"
- Cliquer sur "+ Groupes de sécurité d'application"
- Sélectionner votre groupe "asg-tp"
- Cliquer sur "Ajouter"

![vm](https://acenox.fr/memoire/vm1.png)

# Étape 11 : Tester la connexion

- Se rendre dans l'onglet "Connexion"
- Cliquer sur "Télécharger un fichier RDP"
- Puis ouvrez le fichier & renseinez-y vos identifiants de connexion

![vm 2](https://acenox.fr/memoire/vm2.png)

# Étape 12 : Supprimer l'autorisation RDP

Maintenant que nous avons pu voir que cela fonctionne, nous allons tenter de désactiver l'autorisation que nous avons mis en place sur notre NSG.

- Cliquer sur votre machine virtuelle "VM-1"
- Se rendre dans l'onglet "Paramètre réseau"
- Supprimer la règle "allow-rdp"

![NSG2](https://acenox.fr/memoire/nsg2.png)

- Retourner dans l'onglet "connexion"
- Tenter de se connecter en RDP avec la VM

Si vous avez bien suivi toutes les étapes, vous devriez obtenir une erreur lorsque vous tentez de vous connecter en RDP à votre machine virtuelle.

![RDPNOTOK](https://acenox.fr/memoire/rdpnotok.png)

Félicitations ! Vous avez terminé ce premier TP 🥳​

# Aller plus loin

Pour aller plus loin, il est recommandé d'utiliser Azure Bastion pour sécuriser la connexion. De plus, grâce à ce système votre VM n'aura plus besoin d'avoir obligatoirement une IP publique ou d'agent installé pour s'y connecter.

# Étape 13 : Fin du TP - Suppression des ressources

Nous vous conseillons fortement de supprimer vos ressources car comme vu pendant le cours, le paiement se fait à l'utilisation. Vu que nous avons terminé le TP, vous pouvez supprimer.
Pour cela, rien de plus simple il suffit de suivre les étapes suivantes : 

- Rechercher "Groupe de ressources"
- Sélectionner votre Groupe "TP_Azure_1"
- Cliquer sur "Supprimer le groupe de ressources"

![Delete](https://acenox.fr/memoire/supv4.png)
