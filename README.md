Architecture LAN

Mots clés :

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

#Plan d'action :

Etudes :

## Domaine de diffusion, domaine de collision

#### Domaine de collision :

Un domaine de collision est un ensemble d’entités (cartes réseaux) qui partagent le même média de communication. Prenons un exemple dans la vraie vie:
Dans le monde des réseaux, si deux entités sont dans le même domaine de collision et envoient des données à un instant T alors il y a corruption des données et il faut retransmettre les données.

Le domaine de collision dépend de l’équipement sur lequel les entités sont connectés.

#### Doamine de diffusion : 

Dans le monde des réseaux, quand une entité envoi une donnée, elle a le choix entre envoyer la donnée en unicast, en multicast ou en broadcast.
Quand on parle de domaine de broadcast, on prend l’hypothèse où l’entité émétrice souhaite envoyer une donnée à tout le monde, soit en broadcast.

Dans le LAN, que ce soit un Hub, un Bridge ou un Switch, la donnée sera propagée sur tous les ports parce que:

    Un hub ne lit pas le niveau 2 donc il transmet la donnée sur tous ses ports
    Un bridge lit le niveau 2 et comprend que la donnée est a destination de tout le monde (adresse MAC destination = ffff.ffff.ffff) donc elle transmet cette donnée sur son second port
    Un Switch lit aussi le niveau 2 et comprend que la donnée est a destination de tout le monde (adresse MAC destination = ffff.ffff.ffff) donc elle transmet cette donnée sur tous ses ports

Important: le domaine de broadcast s’arrête au niveau d’un équipement niveau 3, comme un routeur !



## Séparer les sous-réseaux
## Architecture 3 couches

Plus généralement nommé par sa version anglaise, « tree-layers hierarchical internetworking design/model », ce modèle a été inventé et diffusé par Cisco.
Ces trois couches sont :
– la couche cœur, « Core layer »
– la couche distribution, « Distribution layer ».
– la couche accès, « Access layer ».

![TLA](https://www.cisco.com/c/dam/en/us/td/i/200001-300000/220001-230000/221001-222000/221701.eps/jcr:content/renditions/221701.jpg)

#### 1) Core Layer

C’est la couche supérieure. Son rôle est simple : relier entre eux les différents segments du réseau, par exemple les sites distants, les LANs ou les étages d’une société.
Nous trouvons généralement les routeurs à ce niveau. Si l’entreprise est vraiment grande, ce modèle peut s’imbriquer : le design d’implémentation des routeurs correspond à ce modèle, mais le design du niveau 2 (modèle OSI), c’est-à-dire les switchs, reprendra la même hiérarchisation et les même rôles ! On a donc un modèle Core/Distribution/Access à l’intérieur de la partie Access ou Distribution des routeurs.
Comme beaucoup de trafic passe par ces routeurs ou switchs Core, les besoins en performance sont conséquents. Et en débit, aussi. Le matériel change donc en fonction du rôle. Par exemple, chez Cisco, le CRS-3 est la référence (322 Tbps, quand même ! Et ce n’est pas donné…).
Le Core est aussi appelé Backbone.

#### 2) Distribution Layer
Une fois nos routeurs/switchs de la couche Core choisis et mis en place dans notre architecture, le designer s’intéresse à la couche Distribution.
Son rôle est simple : filtrer, router, autoriser ou non les paquets… Nous sommes entre la couche Core et la couche Access, c’est-à-dire entre la partie « liaison » et la partie « utilisateurs ». Ici, on commence à diviser le réseau en segment, en ajoutant plusieurs routeurs/switchs de distribution, chacun étant connecté au Core d’un côté, et à la couche Access de l’autre.
Visualisez bien : 1 core router > plusieurs distribution routers connectés sur le même core router > encore plus de switchs access, tous connectés sur une distribution layer. C’est exactement comme un arbre généalogique.
Ici aussi, selon la taille et les moyens de l’entreprise, l’architecte devra choisir entre routeur et switch. Evidemment, plus la société est grande, plus on aura besoin de routeur à ce niveau. Pour une petite entreprise, des switchs suffisent.
Ces routeurs de distribution vont s’occuper de router les paquets, d’y appliquer des ACLs, d’assurer la tolérance de panne, de délimiter les domaines de broadcast, etc…
Note : Bien entendu, s’il n’y a que des switchs dans notre couche distribution, ces actions seront effectuées au niveau Core puisque seule la couche Core possède des routeurs.
On peut aussi, comme vous le trouverez probablement dans certains articles sur Internet, résumer le rôle de la couche Distribution en disant qu’elle sert à relier les couche Core et Access.

#### 3) Access Layer

C’est la dernière couche de notre modèle. Son rôle est simple mais très important : connecter les périphériques « end-users » au réseau.
Mais aussi, assurer la sécurité !
Ici, pas de routeur. Seuls des switchs, ou hubs parfois, sont implémentés. C’est normal, me direz-vous, puisque tout le travail des routeurs est déjà effectué au niveau de la Distribution ou du Core. Résultat, on ne s’occupe que de connecter nos end-users au réseau, que ce soit en Wi-fi, Ethernet ou autre. Et si possible, on le fait de manière sécurisée, c’est-à-dire en utilisant switchport sur nos switchs, en désactivant les interfaces non utilisées, etc…
Du coup, la configuration de ce type de switch pose moins de contrainte. Pas besoin de performances particulières car chaque switch aura – au maximum – un nombre d’utilisateur égale à son nombre de port (moins 1 ou 2 pour le trunk entre Access et Distribution). De plus, les traitements restent basiques et ne demandent que peu de ressources.

#### 4) Mais encore ?…

Il est important de noter que chaque couche apporte ses impératifs et ses besoins, influençant le matériel mis en place ainsi que  les configurations et/ou solutions.
C’est d’ailleurs la raison principale de l’existence de ce modèle : plus compliqué, au premier abord, à mettre en place, mais totalement plus efficace, rentable, réfléchi et économe sur le long terme qu’une architecture improvisé au fil du temps.


## VLSM

Voir cisco ccent 1

## Configurer les switches de façon sécurisée (VTP, port)

![](/ress/1.png)
![](/ress/2.png)
![](/ress/3.png)
![](/ress/4.png)
![](/ress/5.png)
![](/ress/6.png)
![](/ress/7.png)

## VLAN

Un VLAN (Virtual Local Area Network ou Virtual LAN, en français Réseau Local Virtuel) est un réseau local regroupant un ensemble de machines de façon logique et non physique.

En effet dans un réseau local la communication entre les différentes machines est régie par l'architecture physique. Grâce aux réseaux virtuels (VLANs) il est possible de s'affranchir des limitations de l'architecture physique (contraintes géographiques, contraintes d'adressage, ...) en définissant une segmentation logique (logicielle) basée sur un regroupement de machines grâce à des critères (adresses MAC, numéros de port, protocole, etc.).

Plusieurs types de VLAN sont définis, selon le critère de commutation et le niveau auquel il s'effectue :

    Un VLAN de niveau 1 (aussi appelés VLAN par port, en anglais Port-Based VLAN) définit un réseau virtuel en fonction des ports de raccordement sur le commutateur ;
    Un VLAN de niveau 2 (également appelé VLAN MAC, VLAN par adresse IEEE ou en anglais MAC Address-Based VLAN) consiste à définir un réseau virtuel en fonction des adresses MAC des stations. Ce type de VLAN est beaucoup plus souple que le VLAN par port car le réseau est indépendant de la localisation de la station ;
    Un VLAN de niveau 3 : on distingue plusieurs types de VLAN de niveau 3 :
        Le VLAN par sous-réseau (en anglais Network Address-Based VLAN) associe des sous-réseaux selon l'adresse IP source des datagrammes. Ce type de solution apporte une grande souplesse dans la mesure où la configuration des commutateurs se modifient automatiquement en cas de déplacement d'une station. En contrepartie une légère dégradation de performances peut se faire sentir dans la mesure où les informations contenues dans les paquets doivent être analysées plus finement.
        Le VLAN par protocole (en anglais Protocol-Based VLAN) permet de créer un réseau virtuel par type de protocole (par exemple TCP/IP, IPX, AppleTalk, etc.), regroupant ainsi toutes les machines utilisant le même protocole au sein d'un même réseau.

Les VLAN sont définis par les standards IEEE 802.1D, 802.1p, 802.1Q et 802.10. Pour plus d'information il est donc conseillé de se reporter aux documents suivants :
    IEEE 802.1D
    IEEE 802.1Q
    IEEE 802.10

Les configurations sont stockées dans un fichier de base de données VLAN nommé vlan.dat. Le fichier vlan.dat se trouve dans la mémoire Flash du commutateur.

Réaliser :

## Proposer une architecture adaptée


