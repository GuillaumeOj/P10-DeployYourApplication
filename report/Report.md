---
title: Projet 10 - Déployez votre application sur un serveur comme un pro ! 
subtitle: Parcours OpenClassrooms - Développeur d'application Python
author:
  - 'Étudiant : Guillaume OJARDIAS'
  - 'Mentor : Erwan KERIBIN'
  - 'Mentor évaluateur : Benoît PRIEUR'
geometry: margin=1.5cm
---
\renewcommand{\contentsname}{Sommaire}
\tableofcontents

\pagebreak
# I. Présentation

Ce projet se base sur le projet 8 : _[Créez une plateforme pour les amateurs de Nutella](https://openclassrooms.com/fr/paths/68/projects/159/assignment)_.

L'objectif principal de ce projet et de déployer l'application du projet 8 sur un serveur paramétré par nos soins. Pour cela nous devons mettre en œuvre les éléments suivants :
- un outil d'intégration continue type [Travis](https://travis-ci.com/),
- déployer l'application sur un serveur du même type que ceux proposés pas [Digital Ocean](https://www.digitalocean.com/),
- un outil de monitoring permettant le suivi des performances du serveur,
- un système de logging pour surveiller les logs de l'application du type [Sentry](https://sentry.io/welcome/),
- créer un tâche CRON pour la mise à jour de la base de données de l'application à raison d'une fois par semaine,
- et enfin utiliser un nom de domaine (optionnel).

## I.1. Liens du projets

- Le site est visible en ligne à cette adresse : _[http://projet-10.ojardias.io/](http://projet-10.ojardias.io/)_.

# II. Démarche de création

## II.1. Mise en place du serveur

- Création d'un Droplet Digital Ocean à l'adresse [http://167.172.169.38](http://167.172.169.38) :
- Mise en place de la connexion SSH, mise à jours des packages du serveur et création d'un utilisateur `guillaume` :
- Installation de `python3`, `postgresql`, `git`, `nginx` et `supervisor`.
- Clone du [repository](https://github.com/GuillaumeOj/Pur-Beurre) dans le répertoire `/home/guillaume/pur-beurre`. 
- Paramétrage du pare-feu `UFW` :

![Configuration de UFW](img/01-UFW-Status.png){ width=300px }

- Configuration de NGINX et Supervisor :

![Configuration de NGINX](img/02-Configuration-NGINX.png){ width=300px }

![Configuration de supervisor](img/03-Configuration-Supervisor.png){ width=300px }

\pagebreak
- Création de tâches CRON

![Mise en place de tâches CRON](img/04-Cron-tasks.png){ width=300px }


## II.2. Mise en place du CI

- Configuration de Travis pour la partie Continuous Integration :

![Configuration de Travis](img/05-Configuration-Travis.png){ width=300px }

- Mise en place et configuration de Mergify pour le merge des Pull Requests :

![Configuration de Mergify](img/06-Configuration-Mergify.png){ width=300px }


\pagebreak
## II.3. Monitoring de l'application

- Configuration de Sentry pour le reporting des issues non gérées par l'application :

![Dashboard de Sentry](./img/07-Dahsboard-Sentry.png){ width=300px }

- Mise en place d'un monitoring du Droplet en utilisant les outils mis à disposition par Digital Ocean :

![Monitoring Digital Ocean](./img/08-Monitoring-Digital-Ocean.png){ width=300px }

# III. Bilan

## III.1. NGINX et Supervisor

La combinaison de ces deux outils permet de mettre en place très rapidement avec une configuration minimaliste un serveur fonctionnel.
Cependant, j'ai dû faire face à deux difficultés pour la configuration de ces deux services.

Je souhaitais héberger d'autres applications sur ce serveur, mon CV en  ligne (https://guillaume.ojardias.io) par exemple. Après quelques tâtonnements et essais infructueux, j'ai fini par comprendre qu'il suffisait simplement de rediriger chaque application sur un port local unique. Raison pour laquelle l'application du projet 8 est redirigée vers le port 8001 (et non 8000 par défaut).

Ensuite, je tenais à mettre en place des certificats SSL. Après un premier essai catastrophique, dans la panique j'ai complètement réinitialisé mon serveur à zéro, j'ai fini par comprendre qu'il me manquait une étape cruciale. Modifier les `Nameservers` de mon fournisseur de nom de domaine vers ceux de Digital Ocean, j'ai finit par réussir à avoir une configuration qui fonctionne.

## III.2. Travis, Sentry et Monitoring

Même si ces trois outils n'ont pas forcément de rapport les uns avec les autres, je me suis permis de les regrouper. En effet, je n'ai pas eu de difficultés particulière quand à leur utilisation (dans le cadre de mon stage, nous utilisons [CircleCi](https://circleci.com/) et [Sentry](https://sentry.io/)).

Sentry m'a permis toutefois de mettre en avant un bug non géré est embêtant sur mon application du projet 8. Un bug sur les templates des erreurs `4xx` et `5xx`. Et j'ai pu ainsi apporter un correctif.

## III.3. Mergify

Pour finir, un dernier mot sur l'utilisation de Mergify pour compléter le processus de Continuous Integration. J'ai découvert cet outil par le biais de mon stage chez l'éditeur [Mergify](https://mergify.io). Travaillant dessus et l'utilisant au quotidien, je ne pouvais pas mettre un système de pull-request sur mon repository sans au final utilisé ce plugin permettant de merger mes pull-requests une fois les conditions paramétrées remplies.

Dans le cadre de ce projet, la pull-request est mergée dans la branche master une fois que les build Travis ont le statut `success` et sans review à partir du moment où je suis l'auteur de la pull-request.

## III.4 Conclusion

Pour conclure, je suis très content des sujets que j'ai pu aborder au cours de ce projet. C'est en quelque sorte la "dernière" brique d'un projet permettant de gérer un projet de sa conception à sa mise en production en passant par sa réalisation.

La dernière chose que j'aimerais faire pour améliorer mon workflow et être dans une dynamique de Continuous Integration / Continuous Deployement, c'est de mettre en place un outil permettant de déployer automatiquement mes applications lorsque la branche master du repository est mise à jour.
