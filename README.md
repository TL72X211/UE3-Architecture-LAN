


# Architecture LAN

## Mots clés :

- **Commutateur :** ou Switch, est un équipement qui relie plusieurs segments dans un réseau informatique, et qui permet de créer des circuits virtuels, c'est à dore interconnecter plusieurs cartes d'interface ensemble. Il s'occupe d'acheminer les trames sur le port physique concerné. On retrouve la commutation et le routage, il dispose d'une table d'adresse MAC, qu'il construit dynamiquement avec les @MAC des ports correspondants.
- **Domaine de diffusion :** ou Broadcast, consiste à transmettre à tous les autres ordinateurs du même domaine sans passer par un routeur.
- **Réseau local :** ou LAN (Local Area Network) est un réseau informatique dont les composants (ordinateurs) s'échangent des trames sans utiliser d'accès à internet.
- **Architecture en 3 couches :** Etudié par la suite
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

### II -  Le modèle en trois couches
Un bon architecte réseau se doit de mettre en place en priorité les performances, le coût, la tolérance de panne, la rapidité des échanges...
Le modèle des trois couches (Tree layers Hierachical Internetworking design/model) inventé et diffusé par Cisco a pour but de créer un design réseau structuré en trois couches.

Ces trois couches sont :

- Coeur (Core Layer)
- Distribution (Distribution Layer)
- Accès (Access Layer)

http://bibabox.fr/wp-content/uploads/2011/08/schema.jpg

**1- Core Layer (ou Backbone)**

Relier entre eux les différents segments du réseau, besoin de grandes performances car de nombreux trafics passent par dedans. On y retrouve généralement des routeurs, ou des switch.

**2 - Distribution Layer**

Filtrer, router, autoriser (ou non les paquets), c'est la partie liaison et la partie utilisateur. Il faut divier le réseau en segment en ajoutant plusieurs routeurs * switch de distribution, chacun étant connecté au coeur et à la couche accès. Pour une grande entreprise -> Routeur, sinon des switch suffisent.

**3 - Access Layer**

Connecter les périphériques "end-users" au réseau, que ce soit en Wi-fi, Ethernet, ou autre...
Elle nécessite de la part de l'administrateur certaines actions (réglage de l'état de chaque port des switchs, mises en place de sécurités...) 

### III - Séparer son réseau - VLAN

Virtual Local Area Network.
De nos jours, quand on connecte un appareil, il se configure automatiquement (notamment pour les switch), c'est ce qu'on appelle le plug and play.

Cependant si l'on souhaite que certains PC ne communiquent pas avec d'autres, il est nécessaire de faire des VLAN. Séparer son réseau avec les VLAN revient donc à découper son Switch en plusieurs Switch.

**VLAN de couche 1 : Configuration de ports**

On créer le VLAN sur le switch, puis on attribue ce VLAN sur les ports souhaités. 
Un **tag** de 4 octet est ajouté à la trame ethernet. 
Ce **tag** comprend entre autre l'identifiant de VLAN. Ainsi, la trame sera transmise uniquement aux ports appartenant au vlan identifié dans la trame.

*Ex: On définit que les ports de 1 à 10 soient sur le VLAN 1 et 11 à 20 sur VLAN 2*

**VLAN de couche 2 : VLan par @MAC**

On configure le switch pour qu'il récupère l'@ MAC qu'il voit transiter  sur le port, envoi cette @MAC vers un serveur VMPS (VLAN Membership Policy Server) qui fera le lien entre l'@ MAC et le VLAN dans une base de données. C'est le serveur VMPS qui indique au Switch quel VLAN il faut attribuer au port.
\!/ Tout passe par le serveur, et s'il est en panne, tout tombe en panne.

**VLAN de couche 3 :** (Le plus utilisé)
- VLAN par sous réseau ==> VLAN 1 =   192.168.0.1/24 && VLAN 2 = 192.168.1.0/24
- VLAN par protocole (IP, IPX, Apple Talk...)

**Nota Bene :**

- VLAN 0 et 4095 = Réservé pour le système
- VLAN 1 = VLAN par défaut, **réservé pour l'administration par convention**
- VLAN 2 - 1001 = VLAN Ethernet (Plage standard)
- VLAN 1002  - 1005 = Technologies FDDI et Token Ring (Sont réservés, ce sont d'anciens protocoles réseau)
- VLAN 1006 - 4094 = VLAN Ethernet - Plage étendue (Utilisé pour les WAN, utilisé par les FAI)
- Les VLAN ne peuvent pas communiquer ensemble
- Chaque VLAN est indépendant (Chaque modif est à faire sur chaque VLAN)
- Chaque VLAN doit-être adressé
- Un port ne peut a voir qu'un seul VLAN

**CONFIGURER SON VLAN**

Il existe plusieurs types de configurations pour les ports :
- Mode access (Connexion terminale appartenant à un seul VLan)
- Mode Trunk (Plusieurs VLAN doivent circuler sur un même lien, comme liaison entre deux switchs, ou un serveur qui à une interface appartenant à plusieurs VLAN)
- Si VLAN crée et affecté à aucun port, c'est un VLAN de management, on y attribue une @IP

\!/ à un VLAN crée, on attribue un sous-réseau IP dédié.

*Configuration complète ici :*

https://reussirsonccna.fr/comment-separer-son-reseau-avec-les-vlan/

http://www.clemanet.com/switch-vlan-cisco.php

**AVANTAGES**
- Gain de sécurité
- Facilite l'administration
- Gain de fluidité (trafic réseau), éviter les "tempêtes de broadcast".

**NORMES**
- IEEE 802.1D
- IEEE 802.1p
- IEEE 802.1Q (la plus importante, permet encapsuler les trames).
- IEEE 802.10

### IV - 


