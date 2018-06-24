# Guide pour du Live Streaming vidéo de Kin-Ball

Ce guide a pour but de partager toutes les informations qui sont utiles pour diffuser un live vidéo d'un match (de Kin-ball ou autre sport collectif).

## Matériel

### Live avec des caméra(s) ou appareil(s) photo

De nombreuses caméras disposent d'un port HDMI permettant de sortir un signal vidéo sur un autre appareil.

Quelques éléments à vérifier lors du choix de l'appareil:

* Supprimer la veille automatique (et toute autre fonctionnalité d'économie d'énergie)
* Désactiver l'affichage des paramètres dans le signal vidéo sortant (souvent à partir d'un bouton display ou dans le menu de l'appareil)
* Vérifier si l'appareil a besoin d'un adaptateur mini- ou micro HDMI
* Disposez-vous d'un adaptateur secteur ou de batteries suffisantes pour ne pas devoir interrompre le Live ?

#### Carte de capture vidéo

Pour utiliser le signal vidéo sur un ordinateur, il faut une carte vidéo. Un élément non-négligeable est de vérifier si l'ordinateur qui diffusera le live dispose du bon port selon la carte choisie.

Voici une petite liste de carte de capture non ex-haustive.

**Blackmagic UltraStudio Mini ~165 €**

* Sortie DisplayPort
* Limité à 1080p

![Blackmagic UltraStudio Mini](https://static.bhphoto.com/images/images500x500/Blackmagic_Design_bdlkulsdzminrec_Ultrastudio_Mini_Recorder_1348246032000_892453.jpg)

**Elgato CAM LINK ~ 130 €**

* Sortie USB
* Limité à 1080p

Attention l'adaptateur n'est [compatible qu'avec un nombre limité de caméras](https://www.elgato.com/en/gaming/cam-link/camera-check) !

![Elgato CAM LINK](https://media.ldlc.com/ld/products/00/04/77/44/LD0004774465_2.jpg)

**Magewell USB Capture HDMI Plus ~360 $**

* Sortie USB
* Limité à 1080p

**Inogeni USB 3.0 4K HDMI ~395 $**

* Sortie USB 3.0

![INOGENI USB 3.0 4K HDMI](https://static.bhphoto.com/images/images500x500/inogeni_4k2usb3_4k_hdmi_to_usb_1431530477000_1073122.jpg)

#### Matériel à prévoir

* Appareil photo ou caméra
* Adaptateur micro ou mini-HDMI (voir même propriétaire selon l'appareil)
* Câble HDMI
* Carte de capture vidéo
* Rallonges et multiprises

### Live avec un smartphone

Il est possible d'utiliser le flux vidéo d'un smartphone grâce par exemple à l'application IP Webcam qui diffuse localement le signal vidéo et que l'on peut récupérer sur un ordinateur qui est sur le même réseau.

Un tutoriel avec le logiciel OBS très explicite se trouve ici: [How to Live stream your Laptop Webcam and Iphone for 1$](https://medium.com/@petterik_/how-to-live-stream-with-your-laptop-webcam-and-iphone-for-1-39938d33d19d)

## Logiciel

### OBS Studio

C'est l'un des logiciels les plus puissant dans ce domaine. Il est en plus gratuit et open source !

Le fonctionnement est assez simple et flexible. Lors du Live, il est possible de changer de scène. Chaque scène peut contenir plusieurs sources. Généralement, on aura une scène par caméra ainsi que des scènes avec des caméras à double où l'on vient ajouter des sources spécifiques comme le programme de l'événement (par ex. entre plusieurs matchs).

Pour sa prise en main, se référer aux nombreux tutoriels disponible sur Youtube ou tout autre site.

### Difusion

OBS est déjà pré-configuré avec un certain nombre de plateforme comme Facebook, Youtube, Twitch, etc.

Une chose importante à définir en amont est la plateforme de diffusion. On l'a choisi selon son audience bien sûr, mais il y a aussi quelques paramètres techniques à prendre en compte. Par exemple Facebook (à l'heure actuelle - juin 2018), permet de faire des Live d'une durée maximum de 4 heures contrairement à Youtube.

Il existe des services payants permettant de diffuser simultanément sur plusieurs plateformes comme :

* [Restream](https://restream.io/)
* [Switchboard](https://switchboard.live)

#### Youtube

A prévoir, il faut activer la fonction Live sur le compte Youtube au moins 24h à l'avance: [Support Youtube - Activer la fonctionnalité sur votre chaîne](https://support.google.com/youtube/answer/2474026?hl=fr&ref_topic=6136989)

### Idées pour intégrer un tableau de scores

La principale difficulté pour le Live est l'intégration du score des matchs en incrustation. Comme il n'existe pas de réelle façon de faire, j'ai testé et envisagé plusieurs techniques:

#### 1. Interface Web entièrement

C'est la technique qui a été utilisé lors de la [Journée de Championnat n°12 2018](https://www.youtube.com/watch?v=KtFbmAnE4wY)

Comme OBS intègre un source vidéo de type navigateur, il est possible d'ajouter une page web par-dessus une flux vidéo. La transparence étant également bien gérée.

| Avantages     | Désavantages  |
| ------------- |-------------|
| Performance      | Lors du changement de match, il faut être bien préparer pour avoir les données sous la main |
| Simplicité, pas besoin d'un serveur pour héberger la page web      | Nécessite un rechargement de la page lors du changement de match      |
| Pas de latences | Pas de sauvegarde/backup du score      |
| | Editions des données dans du JSON, ce qui n'est pas très user-friendly |

Les fichiers utilisés se trouvent dans [1_WebOBS_Interface](1_WebOBS_Interface)

##### Améliorations

Bugs:

* Mac OS: plusieurs bugs sont à noter:
  * Imposible de redimensionner la fenêtre "interagir" (OBS version 21.1.1), ce qui rend difficile l'utilisation du sélecteur de caméra et de cette fenêtre sur un seul même écran
  * L'attribut HTML "contenteditable" n'est pas supporté, il faudrait convertir ou rajouter des champs de formulaires (input). L'idée avec cet attribut est de pouvoir modifier un score ou un nom d'équipe directement depuis OBS sans devoir recharger la page.

Au niveau de l'interface:

* L'interface automatise le gain des périodes lorsqu'une équipe a 13 points. Malheureusement, il arrive de faire des erreurs d'équipe lorsque l'on rentre les points et avec ce système, il manque un moyen de revenir en arrière facilement.
* Un système plus efficace serait peut-être d'avoir une page sous forme de tableau éditable en utilisant une librairie comme [Handsontable](https://handsontable.com/) ou [DHTMLX Grid](https://dhtmlx.com/docs/products/dhtmlxGrid/)

#### 2. Interface Excel/Libre Office

La deuxième idée est d'utiliser une feuille de calcul qui contiendrait les données du match en cours et du programme des matchs.
Pour rendre cette idée utilisable sur tous les systèmes d'exploitation, le choix a été d'utiliser Libre Office Calc.

Le système est utilisable, mais il faut être conscient que:

* Il y a des problèmes de performance notamment sur Mac OS avec LibreOffice Calc
* L'interface ne donne pas le sentiment d'être bien conçue (scintillement).

Les fichiers utilisés se trouvent dans [2_LibreOffice_Interface](2_LibreOffice_Interface)

Pour les faire fonctionner, il faut activer les macros dans Libre Office (ce qui permet le rafraîchissement des données):

[Libreoffice - preferences - securité](https://help.libreoffice.org/Common/Security_Warning/fr)

#### 3. Utiliser l'API Google Spreadsheets

Une troisième possibilité vaguement testée serait d'utilser une feuille de calcul Google Spreadsheets et de récupérer les données via leur API gratuite. Seulement avec cette technique, il y a un problème qui peut apparaître:
l'API ne permet pas de pousser les données une fois un changement effectué. Le système doit alors récupérer tous les temps de temps celles-ci avec une limitation de l'API à toutes les 2 secondes. Selon la connexion, il est possible aussi que la sauvegarde de document (qui se fait automatiquement) soit ralentie et de manière très aléatoire sans prévenir l'utilisateur.

Néanmoins, il est possible d'utiliser une seconde API, celle de Google Drive qui permet de pousser les données avec un système de Webhook. A investiguer !

#### 4. Utiliser une base de donnée temps réelle

Une autre hypothètique solution serait d'utiliser une base de données en temps réelle. L'idée est surtout utile si on veut un système plus évolué qui afficherait le score à plusieurs endroits autant sur le live que sur un site internet.

Un exemple avec le framework Vue.js: [https://firebase.googleblog.com/2016/04/vuefire-firebase-meets-vuejs_0.html](https://firebase.googleblog.com/2016/04/vuefire-firebase-meets-vuejs_0.html)

#### 5. Application/service spécialisé(e) pour overlay (souvent payant)

Après de longues recherches, je n'ai pas trouvé de services proposant ce genre de système, bien qu'il existe des systèmes de points pour les gamers aucun service ou application n'a été assez convaincante ou assez flexible pour permettre la personnalisation du thème.

## A ajouter dans ce guide

* Partie Audio