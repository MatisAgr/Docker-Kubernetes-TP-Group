# Projet fil rouge
Tisma : [![wakatime](https://wakatime.com/badge/user/a16f794f-b91d-4818-8dfc-d768ce605ece/project/59bc72bd-08ec-4546-82f7-6787e0097c41.svg)](https://wakatime.com/badge/user/a16f794f-b91d-4818-8dfc-d768ce605ece/project/59bc72bd-08ec-4546-82f7-6787e0097c41) + [![wakatime](https://wakatime.com/badge/user/a16f794f-b91d-4818-8dfc-d768ce605ece/project/49383522-39f2-4b66-b600-59671bf3575f.svg)](https://wakatime.com/badge/user/a16f794f-b91d-4818-8dfc-d768ce605ece/project/49383522-39f2-4b66-b600-59671bf3575f)

## Introduction

Ce projet est une application microservices construite avec Node.js et React. Il est conçu pour être déployé sur Kubernetes.

## Table des matières

- [Introduction](#introduction)
- [Table des matières](#table-des-matières)
- [Architecture](#architecture)
- [Chemins d'Ingress](#chemins-dingress)
- [Noms de Services Kubernetes](#noms-de-services-kubernetes)
- [Ports des Services](#ports-des-services)
- [Prérequis](#prérequis)
- [Installation](#installation)
- [Déploiement](#déploiement)

## Architecture

L'application est composée des services suivants :

- **Client** : Interface utilisateur construite avec React.
- **Posts** : Service pour la gestion des posts.
- **Comments** : Service pour la gestion des commentaires.
- **Query** : Service pour la gestion des requêtes.
- **Moderation** : Service pour la modération des commentaires.
- **Event Bus** : Service pour la gestion des événements entre les services.

### Chemins d'Ingress

- `/posts/create` : Dirigé vers le service `ms-posts-srv` sur le port 4000.
  - Utilisé pour créer de nouveaux posts.
  
- `/posts` : Dirigé vers le service `ms-query-srv` sur le port 4002.
  - Utilisé pour récupérer la liste des posts existants.
  
- `/posts/?(.*)/comments` : Dirigé vers le service `ms-comments-srv` sur le port 4001.
  - Utilisé pour créer ou récupérer les commentaires associés à un post spécifique.
  
- `/?(.*)` : Dirigé vers le service `ms-client-srv` sur le port 3000.
  - Utilisé pour accéder à l'interface utilisateur.
 


### Noms de Services Kubernetes

Assurez-vous que les noms de services dans vos fichiers de déploiement Kubernetes correspondent aux noms de services utilisés dans le code de l'application. Voici les noms de services attendus :

- **ms-client-srv**: Service pour l'interface utilisateur.
- **ms-posts-srv**: Service pour la gestion des posts.
- **ms-query-srv**: Service pour la gestion des requêtes.
- **ms-comments-srv**: Service pour la gestion des commentaires.
- **ms-moderation-srv**: Service pour la modération des commentaires.
- **ms-event-bus-srv**: Service pour la gestion des événements entre les services.

Si vous modifiez ces noms, assurez-vous également de mettre à jour les références correspondantes dans le code de l'application.


### Ports des Services

Chaque service écoute sur un port spécifique. Assurez-vous que ces ports sont correctement configurés dans vos fichiers de déploiement Kubernetes et dans tout autre outil de gestion des conteneurs que vous pourriez utiliser. Voici les ports attendus pour chaque service :

- **ms-client-srv**: Écoute sur le port 3000.
- **ms-posts-srv**: Écoute sur le port 4000.
- **ms-query-srv**: Écoute sur le port 4002.
- **ms-comments-srv**: Écoute sur le port 4001.
- **ms-moderation-srv**: Écoute sur le port 4003.
- **ms-event-bus-srv**: Écoute sur le port 4005.

Si vous modifiez ces ports, assurez-vous également de mettre à jour les références correspondantes dans le code de l'application et les fichiers de configuration Kubernetes.


## Prérequis

- Node.js
- Docker
- Kubernetes

## Installation

1. Clonez ce dépôt :
    ```bash
    git clone https://github.com/Mossbaddi/Pojet_fil_rouge.git
    ```

2. Installez les dépendances pour chaque service :
    ```bash
    cd client && npm install
    cd ../posts && npm install
    # Répétez pour tous les services
    ```

## Déploiement

1. Construisez les images Docker pour chaque service :
    ```bash
    docker build -t client ./client
    docker build -t posts ./posts
    # Répétez pour tous les services
    ```
    Le projet est basé sur l'image **node:alpine**

2. Déployez les services sur Kubernetes :
    ```bash
    kubectl apply -f k8s/
    ```
