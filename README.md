#Architecture LAN

##Mots clés :

- Commutateur
- Domaine de diffusion
- Réseau local
- Architecture en 3 couches
- Trafic inutile
- Données liées à l'administration
- Données en clair
- Plage IP
- Adresse d'administration
- Traitement heuristique

##Contexte :

Quoi ?

- Architecture LAN
- Administration des commutateurs

Comment ?

- En analysant le trafic du réseau
- Faire des maquettes
- Reconfigurant les switches
- Découper les plages IP

Pourquoi ?

- Diffusion trop importante des trames
- Les données passent en clair
- Même plage IP

##Problématique :

- Comment réduire le trafic sur un réseau LAN ?

- Comment découper une LAN et traité les données de manière sécurisée ?

Généralisation :

- Reconception

##Hypothèse :

- Créer des sous-réseaux
- Réaliser un schéma d'adressage
- Analyser le trafic
- Reconfigurer les switches
- Tempête de broadcast
- Redondance
- Créer des groupes de diffusions

##Plan d'action :

##Etudes :

### Domaine de diffusion, domaine de collision
### Séparer les sous-réseaux
### Architecture 3 couches

Modèle hiérarchique en 3 couches, "tree-layers hierarchical internetworking design/model"

Comme le nom l'indique on découpe le réseau en 3 couches, chacune ayant un rôle précis impliquant des différences de matériel, performances et outils

Les trois couches sont : 

- le couche coeur (core layer)
- la couche distribution (distribution layer)
- la couche accès (access layer)

#####**Core layer :**
Elle relie entre eux les différents segments du réseau (sites distants, LANs, étages de la société), il s'agit du backbone

C'est à ce niveau qu'on trouve les routeurs, puisque le trafic est très important à ce niveau les routers et switches doivent être performants.

#####**Distribution layer :**

Elle filtre, route et autorise ou non les paquets. On divise le réseau en segments et ajoutant plusiers routeurs/switches de distribution et on connecte chacun au core d'un côté et à la couche Access de l'autre

Si notre couche n'est composé que de switches le routage, la délimitation de domaines de broadcast et l'assurance de la tolérance aux pannes se fera sur la couche Core

#####**Access layer**

Son rôle est simple: connecter les les end-users au réseau et assurer la sécurité

Aucun routeur n'est présent, uniquement des switches ou parfois des hubs. La sécurisation se faire en utilisant **switchport** sur les switches en désactivant les interfaces non utilisées, etc
Les switch n'ont pas besoin de performances particulières, il auront aux max le nombre d'users égal à leur nb de port (1 ou 2 pour la liaison Access-Distribution) et les traitements sont basiques

Ce modèle bien que complexe est efficace et rentable, c'est donc pourquoi il est très utilisé

![](picsNico/3couches.jpg)

### VLSM

Avec la méthode classique de segmentation en sous-réseaux (A, B, C, D), le même nombre d'adresses est attribué à chaque sous-réseau. Cette répartition résulte très souvent en un gaspille d'adresses, c'est pourquoi on à recourt au VLSM

Avec le VLSM (Variable Length Subnet Mask) on peut découper un réseaux en sous réseaux de tailles différentes afin de correspondre au mieux au nombre de postes nécessaires 

![](picsNico/VLSM.jpg)

Pour découper un réseaux à l'aide du VLSM on commence avec le plus grand sous réseaux et on découpe le réseau pour répondre au nombre de postes nécessaires ((2^nb de bits partie hôte)-2) plus une éventuelle marge (penser à l'évolutivité) on découpe ensuite les sous-réseaux restants pour satisfaire tous les sous-réseaux jusqu'au plus petit. Pour utiliser le VLSM on doit donc savoir le nombre de sous réseaux et la taille de chaque sous réseaux


### Configurer les switches de façon sécurisée (VTP, port)
### VLAN

##Réaliser :

### Proposer une architecture adaptée


