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

![Dashboard de Sentry](img/07-Dahsboard-Sentry.png){ width=300px }

- Mise en place d'un monitoring du Droplet en utilisant les outils mis à disposition par Digital Ocean :

![Monitoring Digital Ocean](img/08-Monitoring-Digital-Ocean.png){ width=300px }

# III. Bilan

