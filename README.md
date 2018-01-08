

# Architecture LAN

## Mots clés :

- **Commutateur :** ou Switch, est un équipement qui relie plusieurs segments dans un réseau informatique, et qui permet de créer des circuits virtuels, c'est à dore interconnecter plusieurs cartes d'interface ensemble. Il s'occupe d'acheminer les trames sur le port physique concerné. On retrouve la commutation et le routage, il dispose d'une table d'adresse MAC, qu'il construit dynamiquement avec les @MAC des ports correspondants.
- **Domaine de diffusion :** ou Broadcast, consiste à transmettre à tous les autres ordinateurs du même domaine sans passer par un routeur.
- **Réseau local :** ou LAN (Local Area Network) est un réseau informatique dont les composants (ordinateurs) s'échangent des trames sans utiliser d'accès à internet.
- **Architecture en 3 couches :** ou Architectures trois tiers, est une architecture logique du système divisé en trois couches : Présentation (Affichage), traitement et accès aux données. Cette architecture est basée sur l'environnement client-server. (Client, Application, Base de données).
- **Trafic inutile :**/
- **Données liées à l'administration :**/
- **Données en clair :** Données non cryptés
- **Plage IP :**  Plage d'adresse IP
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

### I -  Étude des domaines de diffusion & de collision
**Domaine de collision :**
Deux entités sont dans le même domaine de collision, et envoient des données à un instant T, alors il y a corruption des données. (Ex : Plusieurs personnes parlent sur un Takie-Walkie en même temps)
C'est la zone du réseau d'où proviennent les trames qui entrent en collision.

- Domaine de collision avec le Hub/Concentrateur :
https://reussirsonccna.fr/wp-content/uploads/2012/09/Domaine_collision_Hub-300x214.png
- Domaine de collision avec le Bridge / Pont :
https://reussirsonccna.fr/wp-content/uploads/2012/09/Domaine_collision_Bridge-300x187.png
- Domaine de collision avec le Switch / Commutateur :).
https://reussirsonccna.fr/wp-content/uploads/2012/09/Domaine_collision_Switch-300x202.png

**Domaine de diffusion :** Équivalent du broadcast.

On peut retrouver les deux en mêmes temps (diffusion & collision), notamment avec la présence d'un routeur.

**Ethernet repose sur un algorithme d'accès multiple CSMA/CD**

(Carrier Sense Multiple Access with Collision Detection)

protocole permettant la communication sur un réseau de type Ethernet :

- Commencer à transmettre n'importe quand
- Ne jamais émettre quand détection activité
- Interrompre activité dès détection d'un autre adaptateur sur le même canal (Détection collision)
- Wait() avant de retransmettre une trame

*/ Collision_Emilien.png */

### II -  Comment faire du subnet

### III - L'architecture en trois couches 




