# Lab Github Action
***
![Tidiany](https://img.shields.io/badge/work-on%20progress-red.svg)
![Java](https://img.shields.io/badge/Tidiany-Java-brown)
![Spring Boot](https://img.shields.io/badge/Tidiany-Spring%20Boot-green)
![Github Action](https://img.shields.io/badge/Tidiany-Github%20Action-yellow.svg)
![Docker](https://img.shields.io/badge/Tidiany-Docker-blue)

# Table de matière
1. [Documentation](#documentation)
2. [Vue d'ensemble](#Vue-d-ensemble)
3. [Composants de GitHub Actions](#composants-de-gitHub-actions)
4. [Workflows](#workflows)
5. [Événements](#événements)

# Documentation
Ce projet est un lab pour mettre en place une chaine d'intégration sur un projet Spring Boot avec Github Action et Docker.
En effet ceci est un projet pour mettre en place un pipeline CI/CD avec Github Action...

## Vue d ensemble
GitHub Actions est une plateforme d’intégration continue et livraison continue (CI/CD) qui vous permet d’automatiser votre pipeline de génération, de test et de déploiement. Vous pouvez créer des workflows qui créent et testent chaque demande de tirage (pull request) adressée à votre dépôt, ou déployer des demandes de tirage fusionnées en production.

GitHub Actions dépasse DevOps simplement et vous permet d'exécuter des workflows lorsque d'autres événements se produisent dans votre dépôt. Par exemple, vous pouvez exécuter un workflow pour ajouter automatiquement les étiquettes appropriées chaque fois que quelqu'un crée un problème dans votre dépôt.

GitHub fournit des machines virtuelles Linux, Windows et macOS pour exécuter vos workflows, ou vous pouvez héberger vos propres exécuteurs auto-hébergés dans votre propre centre de données ou infrastructure cloud.

## Composants de GitHub Actions
Vous pouvez configurer un workflow GitHub Actions à déclencher quand un événement se produit dans votre dépôt, par exemple l'ouverture d'une demande de tirage (pull request) ou la création d'un problème. Votre workflow contient un ou plusieurs travaux qui peuvent s'exécuter dans un ordre séquentiel ou en parallèle. Chaque travail s'exécute au sein de son propre exécuteur de machine virtuelle, ou au sein d'un conteneur, et comporte une ou plusieurs étapes qui exécutent un script que vous définissez ou une action, qui est une extension réutilisable qui peut simplifier votre workflow.

![Workflow GitHub Actions](https://docs.github.com/assets/cb-25535/mw-1440/images/help/actions/overview-actions-simple.webp)

### Workflows
Un workflow est un processus automatisé configurable qui exécutera un ou plusieurs travaux. Les workflows sont définis par un fichier YAML archivé dans votre dépôt et s’exécutent lorsqu’ils sont déclenchés par un événement dans votre dépôt, ou ils peuvent être déclenchés manuellement ou selon une planification définie.

Les workflows sont définis dans le répertoire `.github/workflows` d’un référentiel, et un référentiel peut avoir plusieurs workflows, chacun pouvant effectuer un ensemble différent de tâches. Par exemple, vous pouvez avoir un workflow pour générer et tester des demandes de tirage, un autre workflow pour déployer votre application chaque fois qu’une version est créée, et encore un autre workflow qui ajoute une étiquette chaque fois que quelqu’un ouvre un nouveau problème.

>![GitHub Actions Workflows Folder](https://github.com/Tidiany/lab-github-action/blob/main/src/main/resources/static/images/github-workflows-image.png?raw=true)

### Événements
Un événement est une activité spécifique dans un dépôt qui déclenche l'exécution d'un workflow. Par exemple, l'activité peut provenir de GitHub quand quelqu'un crée une demande de tirage (pull request), ouvre un problème ou pousse (push) un commit vers un dépôt. Vous pouvez également déclencher une exécution de workflow selon une planification, en publiant dans une API REST ou manuellement.
Exemple:
***
```bash
on:
  push:
    branches: [ main]
```

### Jobs (travaux)
Un travail est un ensemble d'étapes dans un workflow qui s'exécute sur le même exécuteur. Chaque étape est un script d'interpréteur de commandes qui sera exécuté ou une action qui sera exécutée. Les étapes sont exécutées dans l'ordre et dépendent les unes des autres. Comme chaque étape est exécutée sur le même exécuteur, vous pouvez partager des données d'une étape à une autre. Par exemple, vous pouvez avoir une étape qui génère votre application suivie d'une étape qui teste l'application générée.

Vous pouvez configurer les dépendances d'un travail avec d'autres travaux. Par défaut, les travaux n'ont aucune dépendance et s'exécutent en parallèle entre eux. Lorsqu'un travail prend une dépendance sur un autre travail, il attend que le travail dépendant se termine avant de pouvoir s'exécuter. Par exemple, vous pouvez avoir plusieurs travaux de génération pour différentes architectures qui n'ont pas de dépendances, et un travail d'empaquetage dépendant de ces travaux. Les travaux de génération s'exécutent en parallèle et le travail d'empaquetage s'exécutera quand ils auront fini de s'exécuter.
Exemple:
```bash
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
```

### Actions
Une action est une application personnalisée pour la plateforme GitHub Actions qui effectue une tâche complexe mais fréquemment répétée. Utilisez une action pour réduire la quantité de code répétitif que vous écrivez dans vos fichiers de workflow. Une action peut tirer (pull) votre dépôt git à partir de GitHub, configurer la chaîne d'outils appropriée pour votre environnement de build ou configurer l'authentification auprès de votre fournisseur de cloud.

Vous pouvez écrire vos propres actions ou trouver des actions à utiliser dans vos workflows dans le GitHub Marketplace.

Pour partager des actions au sein de votre entreprise sans les publier publiquement, vous pouvez les stocker dans un référentiel interne, puis configurer celui-ci pour autoriser l’accès aux workflows GitHub Actions dans d’autres référentiels appartenant à la même organisation ou à toute autre organisation de l’entreprise.
Exemple:
```bash
- name: Récuperation du projet...
uses: actions/checkout@v2
```

### Exécuteurs
Un exécuteur est un serveur qui exécute vos workflows quand ils sont déclenchés. Chaque exécuteur peut exécuter un seul travail à la fois. GitHub fournit les exécuteurs Ubuntu Linux, Microsoft Windows et macOS pour exécuter vos workflows. Chaque exécution de workflow s'exécute sur une machine virtuelle nouvellement provisionnée. GitHub propose également des exécuteur plus grand, qui sont disponibles dans des configurations plus grandes. Si vous avez besoin d'un système d'exploitation différent ou d'une configuration matérielle spécifique, vous pouvez héberger vos propres exécuteurs.
```bash
    runs-on: ubuntu-latest
```

### Exemple complet de workflow
GitHub Actions utilise la syntaxe YAML pour définir le workflow. Chaque workflow est stocké en tant que fichier YAML distinct dans votre référentiel de code, dans un répertoire appelé .github/workflows.

Vous pouvez créer un exemple de workflow dans votre dépôt qui déclenche automatiquement une série de commandes chaque fois que du code est poussé (push). Dans ce workflow, GitHub Actions extrait le code envoyé, installe la version 17 de Java avec la distribution temurin, build le projet avec maven et exécute une commande de base pour builder l'image du projet afin de le publier sur Docker Hub toujours en utilisant maven.
```bash
name: build-and-push-image

on:
  push:
    branches: [ main, release ]
    paths-ignore:
      - '**/README.md'
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Récuperation du projet...
        uses: actions/checkout@v2
      - name: Set up JDK 17
        uses: actions/setup-java@v2
        with:
          java-version: '17'
          distribution: 'temurin'
          cache: maven
      - name: Build the project with Maven
        run: mvn -B package
      - name: Build image and Publish to Docker HUB with mvn...
        run: |
          mvn -B spring-boot:build-image -Dspring-boot.build-image.publish=true \
              -Ddocker.user=${{ secrets.DOCKER_USER }} -Ddocker.token=${{ secrets.DOCKER_TOKEN }} \
              -DskipTests
```

Votre nouveau fichier de workflow GitHub Actions est maintenant installé dans votre dépôt et s’exécute automatiquement chaque fois que quelqu’un pousse (push) une modification vers le dépôt. 

Ainsi une fois la validation des modifications et le push éffectuer vers notre dépôt GitHub, la machine se déclanche.

### Illustration:
>**Lancement du build**
> 
![ GitHub Actions Workflows Folder](https://github.com/Tidiany/lab-github-action/blob/main/src/main/resources/static/images/buil-on-github-action-1.png?raw=true)
![ GitHub Actions Workflows Folder](https://github.com/Tidiany/lab-github-action/blob/main/src/main/resources/static/images/buil-on-github-action-2.png?raw=true)
![ GitHub Actions Workflows Folder](https://github.com/Tidiany/lab-github-action/blob/main/src/main/resources/static/images/buil-on-github-action-3.png?raw=true)
![ GitHub Actions Workflows Folder](https://github.com/Tidiany/lab-github-action/blob/main/src/main/resources/static/images/buil-on-github-action-4.png?raw=true)

>**Deploiement sur Docker Hub**
> 
![ GitHub Actions Workflows Folder](https://github.com/Tidiany/lab-github-action/blob/main/src/main/resources/static/images/docker-image-pushed-on-registry.png?raw=true)
