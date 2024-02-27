# Lab Github Action
![Tidiany](https://img.shields.io/badge/work-on%20progress-red.svg)
![Java](https://img.shields.io/badge/Tidiany-Java-brown)
![Spring Boot](https://img.shields.io/badge/Tidiany-Spring%20Boot-green)
![Github Action](https://img.shields.io/badge/Tidiany-Github%20Action-yellow.svg)
![Docker](https://img.shields.io/badge/Tidiany-Docker-blue)

# Documentation

Ce projet est un lab pour mettre en place une chaine d'intégration sur un projet Spring Boot avec Github Action et Docker.
En effet ceci est un projet pour mettre en place un pipeline CI/CD avec Github Action...

## Vue d'ensemble
GitHub Actions est une plateforme d’intégration continue et livraison continue (CI/CD) qui vous permet d’automatiser votre pipeline de génération, de test et de déploiement. Vous pouvez créer des workflows qui créent et testent chaque demande de tirage (pull request) adressée à votre dépôt, ou déployer des demandes de tirage fusionnées en production.

GitHub Actions dépasse DevOps simplement et vous permet d'exécuter des workflows lorsque d'autres événements se produisent dans votre dépôt. Par exemple, vous pouvez exécuter un workflow pour ajouter automatiquement les étiquettes appropriées chaque fois que quelqu'un crée un problème dans votre dépôt.

GitHub fournit des machines virtuelles Linux, Windows et macOS pour exécuter vos workflows, ou vous pouvez héberger vos propres exécuteurs auto-hébergés dans votre propre centre de données ou infrastructure cloud.

## Composants de GitHub Actions
Vous pouvez configurer un workflow GitHub Actions à déclencher quand un événement se produit dans votre dépôt, par exemple l'ouverture d'une demande de tirage (pull request) ou la création d'un problème. Votre workflow contient un ou plusieurs travaux qui peuvent s'exécuter dans un ordre séquentiel ou en parallèle. Chaque travail s'exécute au sein de son propre exécuteur de machine virtuelle, ou au sein d'un conteneur, et comporte une ou plusieurs étapes qui exécutent un script que vous définissez ou une action, qui est une extension réutilisable qui peut simplifier votre workflow.

![Workflow GitHub Actions](https://docs.github.com/assets/cb-25535/mw-1440/images/help/actions/overview-actions-simple.webp)

### Workflows
Un workflow est un processus automatisé configurable qui exécutera un ou plusieurs travaux. Les workflows sont définis par un fichier YAML archivé dans votre dépôt et s’exécutent lorsqu’ils sont déclenchés par un événement dans votre dépôt, ou ils peuvent être déclenchés manuellement ou selon une planification définie.

Les workflows sont définis dans le répertoire .github/workflows d’un référentiel, et un référentiel peut avoir plusieurs workflows, chacun pouvant effectuer un ensemble différent de tâches. Par exemple, vous pouvez avoir un workflow pour générer et tester des demandes de tirage, un autre workflow pour déployer votre application chaque fois qu’une version est créée, et encore un autre workflow qui ajoute une étiquette chaque fois que quelqu’un ouvre un nouveau problème.
