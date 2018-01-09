Architecture LAN

Mots clés :

- Commutateur : Switch, pas d'accès à internet (réservé aux Routeurs)
- Domaine de diffusion : Correspond à une interface du routeur, qui ne relai pas les messages de diffusion. Tout ce qui est dans un domaine reçoit les domaines de diffusion
- Réseau local : Réseau LAN, infrastructure réseau couvrant une zone peu étendue. Souvent administré par une seule entreprise ou personne
- Architecture en 3 couches : AKA "tree-layers hierarchical internetworking design/model", les 3 couches sont Couche **Coeur**, Couche **Distribution**, et Couche **Accès**
- Trafic inutile
- Données liées à l'administration : Mots de passe, noms d'utilisateur etc..
- Données en clair : Données non cryptées (utilisation de TelNet par exemple)
- Plage IP : 192.168.25.1 -- 192.168.25.35 (par ex)
- Adresse d'administration : 
- Traitement heuristique : Traitement rapide et intuitif

Contexte :

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

Problématique :

- Comment réduire le trafic sur un réseau LAN ?

- Comment découper une LAN et traité les données de manière sécurisée ?

Généralisation :

- Reconception

Hypothèse :

- Créer des sous-réseaux
- Réaliser un schéma d'adressage
- Analyser le trafic
- Reconfigurer les switches
- Tempête de broadcast
- Redondance
- Créer des groupes de diffusions

Plan d'action :

Etudes :

- Domaine de diffusion, domaine de collision
	Deux périphériques sont dans le même domaine de collision lorsque l'envoi de données simultané sur la même voix provoque une corruption de ces données.  
	Exemples de domaines de collision :  

	 * Domaine de collision avec un Hub/Concentrateur
	 ![Domaine Collision Hub / Concentrateur](imgFantou/hub_concentrateur.png)

	 * Domaine de collision avec un Bridge
	 ![Domaine Collision Bridge](imgFantou/bridge.png)

	 * Domaine de collision avec un Switch
	 ![Domaine Collision Switch](imgFantou/switch.png)

	Le domaine de diffusion est lui délimité par le type d'équipement présent dans le réseau :
	 * Avec un **Hub**, les messages de diffusion sont transmis car il ne lit pas la couche de niveau 2
	 * Avec un **Brigde**, les messages de diffusion sont transmis car il lit la couche 2 et l'adresse MAC de destination est "ffff.ffff.ffff"
	 * Avec un **Switch**, les messages de diffusion sont transmis car il lit la couche 2 et l'adresse MAC de destination est "ffff.ffff.ffff"
	 * Avec un **Routeur**, les messages de diffusion ne sont pas transmis car il lit la couche de niveau 3 et ne relai pas les messages de broadcast

	Exemples de domaines de diffusion avec Hub, Bridge et Switch :
	 * Hub
	 ![Hub](imgFantou/diffusion_hub_concentrateur.png)

	 * Bridge
	 ![Bridge](imgFantou/diffusion_bridge.png)

	 * Switch
	 ![Switch](imgFantou/diffusion_switch.png)

	**Exemples de domaines de diffusion et de collision :**
	 * Diffusion et Collision via Hub et Switch
	 ![Hub_Switch Collision / Diffusion](imgFantou/hub_switch_collision_diffusion.png)

	 * Diffusion et Collision avec un **routeur**
	 ![Collision / Diffusion avec Routeur](imgFantou/routeur_collision_diffusion.png)

- Séparer les sous-réseaux
	Consiste en découper 'virtuellement' un switch en deux switchs logiques.  
	Il existe trois principales solutions pour définir l'apartenance à un VLAN :
	 * On crée le VLAN sur le switch puis on l'attribue sur les ports souhaités.
	 * On configure le switch pour qu'il récupère l'adresse MAC, il l'envoie à un VMPS (VLAN Membership^Policy Server) qui fait le lien entre VLAN et adresse MAC. Le problème est que si le VMPS tombe en panne, tout le réseau est indisponible.
	 * On utilise la première solution pour les VLAN des PC et le protocole CDP (Cisco Discovery Protocol) pour les téléphones voix sur IP.

	Remarques :
	 * Le VLAN 1 est créé par défaut et tous les ports du switch y appartiennent
	 * On peut donner un nom à un VLAN (optionnel)

	Des plages de VLAN existent et certaines sont réservées :
	  * 0 & 4095 : Réservé pour le système, non utilisable
	  * 1 : VLAN par défaut
	  * 2 - 1001 : VLAN Ethernet
	  * 1002 - 1005 : VLAN créés par défaut pour les technologies FDDI (Fiber Distributed Data Interface) et Token Ring
	  * 1006 - 4094 : VLAN Eternet, plage étendue  


	Configuration :  
	Switch# configure terminal  
	Switch(config)# *vlan* **2**  
	Switch(config)# *name* Administration  
	Switch(config)# end

	Attribution du port à un VLAN :  
	Switch# configure terminal  
	Switch(config)# *interface fastethernet* **0/1**  
	Switch(config-if)# *switchport access* **vlan2**  
	Switch(config-if)# end  
	Switch# show vlan

	Mode Access :

	Mode Trunks :

- Architecture 3 couches
	

- VLSM

- Configurer les switches de façon sécurisée (VTP, port)

- VLAN


Réaliser :

- Proposer une architecture adaptée


