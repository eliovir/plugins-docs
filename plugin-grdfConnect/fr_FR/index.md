# Plugin Grdf-Connect

Plugin permettant la récupération des consommations du compteur communicant *Gazpar* par l'interrogation du compte-client *GRDF*. Les données n'étant pas mises à disposition en temps réel, le plugin récupère chaque jour les données de consommation de gaz de la veille. 

types de consommation accessibles :
- la **consommation journalière** *(en kWh)*.
- la **consommation mensuelle** *(en kWh)*.
- la **consommation annuelle** *(en kWh)*.
- la **consommation publiée vers votre fournisseur gaz** *(péridique en kWh)*.

>**Important**      
>Il est nécessaire d'être en possession d'un compte-client GRDF. Le plugin récupère les informations à partir de la partie *mon espace* <a href="https://monespace.grdf.fr/monespace/particulier/accueil" target="_blank">du site GRDF</a>, il faut donc vérifier que vous y avez bien accès avec vos identifiants habituels(email/mot de passe) et que les données y sont visibles. Dans le cas contraire, le plugin ne fonctionnera pas.

# Configuration

## Configuration du plugin

Le plugin **Grdf-Connect** ne nécessite aucune configuration spécifique mais doit être activé après l'installation.

Deux options sont disponibles dans la configuration du plugin pour gérer la réaction en cas de détecion de captcha à la connexion:
- Ajouter une entrée dans le centre de message (cochée par défaut)
- Désactiver l'équipement 

Vous pouvez également spécifier le nombre de jours de retard généralement constaté afin d'éviter au plugin d'interroger le site pour rien.

Le site GRDF vous permet de spécifier des seuils menusels que le plugin récupère et stocke dans la commande dédiée.
Si vous préférez utiliser les valeurs mensuelles de l'année précédente comme seuils, décochez l'option correspondante.

Les données sont vérifiées toutes les heures entre 4h et 22h et mises à jour uniquement si non disponibles dans Jeedom.

## Configuration des équipements

Pour accéder aux différents équipements **Grdf-Connect**, dirigez-vous vers le menu **Plugins → Energie → Grdf-Connect**.

> **A savoir**    
> Le bouton **+ Ajouter** permet d'ajouter un nouveau compte **Grdf-Connect**.

Sur la page de l'équipement, renseignez l'**identifiant** ainsi que le **mot de passe** de votre compte-client *GRDF* puis cliquez sur le bouton **Sauvegarder**.

Vous pouvez également spécifier le numéro PCE de votre compteur si vous en avez plusieurs liés à votre compte.

Le plugin va alors vérifier la bonne connexion au site *GRDF* et récupérer et insérer en historique :
- **conso journalière** : consommation journalière,
- **conso mensuelle** : consommation mensuelle depuis l'installation du compteur communicant (max 3ans),
- **conso annuelle** : consommation annuelle (somme des mois disponible ou depuis le 1er Janvier),
- **conso publiée** : les 4 dernieres années(avec ou sans compteur communicant),
- **conso (max/min/moy) locale** : consommation mensuelle comparative (maximum/minimum/médiane) des foyers similaires  des 12 derniers mois
- **seuils mensuels** : optionnelle, s'ils sont définis dans votre espace GRDF 

Autre commandes information:
- **coeff de Conversion** : Coefficient de Conversion gaz kWh/m3,
- **Index** : l'index de votre compteur en m3.
- **température** : temperature journaliere moyenne, relevé sur la station méteo la plus proche.
- **Cout jour** : estimation du cout journalier selon les informations configurées.
- **CO2 mensuelle** : estimation Forfaitaire de vos émission Co2, il s'agit bien d'une aproximation.
- **delai MAJ** : delai moyen de disponibilité des donées sur votre compte(en jour), le plugin se sert de cette donée pour évité des requetes inutiles.

# Affichage des informations
Deux tuiles sont disponibles: 
- tuile pérsonalisé; permettant l'affichage des informations  de consommation et les informations comparatives(des 12 derniers mois), il est possible de cacher les informations non souhaités par la procédure habituelle.
- tuile core; cette tuile est géré par le Core Jeedom et vous laisse la possibilité d'apporter vos propres pérsonalisations.

- Le plugin dispose également d'un panel affichant la tuile et des graphiques.

# Recommandations d'usage
- Il faut laisser les commandes en mode "Lissage historique => aucun"
- Eviter d'executer les commandes refresh et oeuvrer à limiter le nombre de requetes.
- **Ne pas poster vos logs sur un fil public, uniquement en MP si nécessaire**

# En cas de dysfonctionnements importants
commencer par vérifier vos ids(email, mdp)
que votre compte et le site grdf sont accessibles en vous connectant dessus.
que votre mdp est conforme aux exigences récentes de grdf(12 caractères, caractères spéciaux…)
que votre version Jeedom est en adéquation avec la version minimal requise par le plugin.

Si des erreurs persistent;
1- Activer les logs en début
2- Faire un refresh ou "sauvegarder l’équipement si les commandes ne sont pas crées, me transmettre les logs complets de cette séquence en MP. 
en cas d’erreur 500 les logs http.error aussi.

PS : !!! Ne pas poster vos logs sur un fil public, **uniquement en MP**, les logs pourraient contenir des informations personnelles directement visibles mais parfois codé !


# Problèmes potentiels

Il se peut que le serveur demande une résolution de captcha pour se connecter.
Ce sera indiqué dans les logs du plugin, dans ce cas, vous devez vous connecter "manuellement" au site GRDF afin de résoudre la captcha.

Comme tout les serveurs, celui de grdf n'est pas infaible, il peut etre momentanement inaccéssible notament pour maintenance...
Le plugin ressaie à intrvales réguliers

En l'abscence d'Api officielle, des changements coté serveur peuvent rendre l'ole plugin innoperant. Je ferais mon maximum pour résoudre ce genre de probleme mais sans garantie.

# Remarques

Le plugin se repose sur la manière dont le site GRDF est structuré. Tout changement sur le site entrainera vraisemblablement une erreur sur le plugin et nécessitera une adaptation de celui-ci plus ou moins difficile à faire.


# Crédits

Ce plugin s'est inspiré entre autes, des travaux réalisés sur le plugin Jazpar.


# Disclaimer

-   En l'abscence d'Api officielle, des changements coté serveur peuvent rendre le plugin innoperant. Je ferais mon maximum pour résoudre ce genre de probleme mais sans garantie.
-   Ce plugin vous est fourni sans aucune garantie. Bien que peu probable, si il venait à corrompre votre installation Jeedom, l'auteur ne pourrait en être tenu pour responsable.

# ChangeLog
Disponible [ici](./changelog.html).
