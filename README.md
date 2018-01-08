
# Architecture LAN

## Mots clés :

- **Commutateur :** ou Switch, est un équipement qui relie plusieurs segments dans un réseau informatique, et qui permet de créer des circuits virtuels. Il s'occupe d'acheminer les trames. On retrouve la commutation et le routage, il dispose d'une table d'adresse MAC, qu'il construit dynamiquement avec les @MAC des ports correspondants.
- **Domaine de diffusion :** ou Broadcast, consiste à transmettre à tous les autres ordinateurs du même domaine sans passer par un routeur.
- **Réseau local :** ou LAN (Local Area Network) est un réseau informatique dont les composants (ordinateurs) s'échangent des trames sans utiliser d'accès à internet.
- **Architecture en 3 couches :** ou Architectures trois tiers, est une architecture logique du système divisé en trois couches : Présentation (Affichage), traitement et accès aux données. Cette architecture est basée sur l'environnement client-server. (Client, Application, Base de données).
- **Trafic inutile :**/
- **Données liées à l'administration :**/
- **Données en clair :** Données non cryptés.
-**Plage IP :**  Plage d'adresse IP
- **Adresse d'administration :** / 
- **Traitement heuristique :** 
en informatique, un algorithme qui permet de résoudre rapidement des problèmes complexes d'optimisation sans se fonder sur une modélisation formelle. Elle n'aboutit pas nécessairement à la solution optimale.

## Contexte :

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

## Problématique :

- Comment réduire le trafic sur un réseau LAN ?

- Comment découper une LAN et traité les données de manière sécurisée ?

## Généralisation :

- Reconception

## Hypothèse :

- Créer des sous-réseaux
- Réaliser un schéma d'adressage
- Analyser le trafic
- Reconfigurer les switches
- Tempête de broadcast
- Redondance
- Créer des groupes de diffusions

## Plan d'action :

Etudes :

- Domaine de diffusion, domaine de collision
- Séparer les sous-réseaux
- Architecture 3 couches
- VLSM
- Configurer les switches de façon sécurisée (VTP, port)
- VLAN

Réaliser :

- Proposer une architecture adaptée

## Réalisation :




