---
title: Projet 10 - Déployez votre application sur un serveur comme un pro ! 
subtitle: Parcours OpenClassrooms - Développeur d'application Python
author:
  - 'Étudiant : Guillaume OJARDIAS'
  - 'Mentor : Erwan KERIBIN'
  - 'Mentor évaluateur : Benoît PRIEUR'
---
\renewcommand{\contentsname}{Sommaire}
\tableofcontents

# Présentation

## Objectif

- Mettre en place un outil de CI
- Déployer son application sur un serveur
- Se servir d'outils de monitoring 
- Savoir créer des tâches programmées
- Utiliser un nom de domaine (optionnel)

## Cahier des charges

- Utiliser un projet existant ([Projet 8](https://projet-8.ojardias.io))
- Ne pas utiliser de plateforme tel qu'Heroku

## Résultat final

- [https://projet-10.ojardias.io](https://projet-10.ojardias.io)

# Démarche de création

## Mise en place du serveur

![NGINX](img/presentation/logo-nginx.png){ width=30px } NGINX : un serveur proxy HTTP

![Supervisor](img/presentation/logo-supervisor.png){ width=30px } Supervisor : un contrôleur de processus système

![Crontab](img/presentation/logo-crontab.png){ width=30px } Cron : programmer l’exécution de scripts

![Python](img/presentation/logo-python.png){ width=30px } Python3

![Postgresql](img/presentation/logo-postgresql.png){ width=30px } Postgresql

## Un workflow complet

![Travis CI](img/presentation/logo-travis.png){ width=30px } Travis : un service d'intégration continue

![Mergify](img/presentation/logo-mergify.png){ width=30px } Mergify : un service d'automatisation des pull-requests

![Sentry](img/presentation/logo-sentry.png){ width=30px } Sentry : un service pour logger les erreurs non gérées

## Points de difficultés

- Plusieurs applications sur un seul serveur
- Mise en place d'un certificat SSL

## Points d'amélioration

- Déploiement automatique sur le serveur
- Commande de mise à jour de la BDD

## Fin

- Merci pour votre attention
