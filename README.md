# 🌌 **Conception et Déploiement d’un Système de Gestion des Âges Étudiants avec Docker et Flask API**

--- 

## 🌟 **Introduction**

### 1.1 **L’Essence du Projet**  
Plongez dans un projet innovant qui allie **esthétique** et **fonctionnalité** : un **Système de Gestion des Âges des Étudiants** conçu avec **Flask API**, **PHP**, et conteneurisé grâce à **Docker**. Ce système offre une expérience fluide pour récupérer et afficher les âges des étudiants via une **API RESTful**, le tout dans une interface web dynamique et visuellement captivante.

### 1.2 **Les Piliers Technologiques**  
- **Flask (Python)** 🐍 : Le cœur de l’API RESTful, orchestrant la gestion des données d’âge avec élégance.  
- **PHP** 🔧 : L’artisan de l’interface web, transformant les données en une expérience visuelle immersive.  
- **Docker** 🐳 : Le maître d’œuvre, encapsulant chaque composant dans des conteneurs pour un déploiement harmonieux.  
- **Docker Compose** 🔄 : Le chef d’orchestre, synchronisant les services pour une performance sans faille.  

### 1.3 **L’Art du Déploiement**  
L’application est déployée avec **Docker**, où **Flask** et **PHP** coexistent dans des conteneurs distincts, communiquant via un réseau en pont Docker. Cette architecture modulaire et évolutive est un véritable chef-d’œuvre de modernité.

---

## 🏛️ **Architecture du Système : Une Symphonie Technologique**

### 2.1 **Vision Globale**  
Le système repose sur une architecture **client-serveur** :  
- Le frontend **PHP** dialogue avec l’API **Flask** pour récupérer les données.  
- L’API **Flask** puise les informations d’âge des étudiants dans un fichier JSON.  
- Les deux services, encapsulés dans des **conteneurs Docker**, interagissent harmonieusement via un réseau partagé.  

### 2.2 **Les Composants Clés**  

- **API Flask (`student_age.py`)** 🌐  
  - Gère les requêtes avec grâce, sécurisant les endpoints par une authentification basique.  
  - Lit et écrit les données dans le fichier `student_age.json`, garantissant une gestion fluide et sécurisée.  

- **Interface Web PHP (`index.php`)** 💻  
  - Récupère les données de l’API Flask via des requêtes HTTP GET.  
  - Utilise l’authentification pour accéder aux endpoints sécurisés.  
  - Transforme les données en une interface web dynamique et visuellement épurée.  

- **Configuration Docker**  
  - **Dockerfile** 📝 : Le plan directeur du conteneur Flask, définissant chaque détail avec précision.  
  - **docker-compose.yml** 📋 : La partition orchestrant l’exécution simultanée des services, créant une symphonie technologique.   

---

## 🛠️ **Structure du Projet**

---

# 📌 **Étape 1 : Construire et Tester l'API**

Dans cette section, nous allons construire et tester notre API Flask en suivant plusieurs étapes.

---

### ✅ **Objectif**

Nous avons utilisé l’image `python:3.8-buster` comme base pour notre conteneur Docker.
Nous avons également ajouté des métadonnées avec `LABEL maintainer` pour indiquer les informations du responsable de l’image Docker.

![azq](https://github.com/user-attachments/assets/e8dbf5a5-7d32-4415-b9fc-f4d20e715810)

---
 
## 📜 **Explication du Dockerfile**

Notre Dockerfile est conçu pour créer une image Docker légère et optimisée pour exécuter une API Python. Voici une explication détaillée de chaque instruction:
Image de Base
dockerfileCopyFROM python:3.8-slim-buster

Utilise l'image Python 3.8 basée sur Debian Buster avec une variante "slim" qui est plus légère que l'image standard
Cette image contient uniquement les composants essentiels de Python, réduisant ainsi la taille de l'image finale

Répertoire de Travail
dockerfileCopyWORKDIR /app

Définit /app comme répertoire de travail dans le conteneur
Toutes les commandes suivantes seront exécutées dans ce répertoire

Installation des Dépendances Système
dockerfileCopyRUN apt-get update -y && apt-get install -y \
    python3-dev \
    libsasl2-dev \
    libldap2-dev \
    libssl-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

Met à jour les listes de paquets et installe les dépendances système nécessaires:

python3-dev: Outils de développement Python
libsasl2-dev: Bibliothèque pour l'authentification SASL
libldap2-dev: Bibliothèque pour LDAP
libssl-dev: Bibliothèque pour SSL/TLS


Nettoie le cache apt et supprime les listes de paquets pour réduire la taille de l'image

Installation des Dépendances Python
dockerfileCopyCOPY requirements.txt .
RUN pip3 install --no-cache-dir -r requirements.txt

Copie le fichier requirements.txt qui liste toutes les dépendances Python
Installe les dépendances avec l'option --no-cache-dir pour éviter de stocker les archives pip, réduisant ainsi la taille de l'image

Copie du Code Source
dockerfileCopyCOPY student_age.py .

Copie le fichier student_age.py qui contient le code source de l'API dans le répertoire de travail

Volume de Données
dockerfileCopyVOLUME /data

Crée un point de montage pour les données persistantes
Les données stockées dans /data persisteront même si le conteneur est supprimé

Exposition du Port
dockerfileCopyEXPOSE 5000

Indique que le conteneur écoutera sur le port 5000
C'est le port sur lequel l'API sera accessible

Commande de Démarrage
dockerfileCopyCMD ["python", "./student_age.py"]

Définit la commande qui sera exécutée au démarrage du conteneur
Utilise la forme exec (tableau) qui est recommandée pour une bonne gestion des signaux

Construire et Exécuter
Pour construire l'image Docker:
bashCopydocker build -t student-age-api .
Pour exécuter le conteneur:
bashCopydocker run -p 5000:5000 -v /chemin/local/vers/data:/data student-age-api
Cette commande:

Mappe le port 5000 du conteneur au port 5000 de l'hôte
Monte un volume local dans le répertoire /data du conteneur


---

## 🚢 **Construction et Lancement du Conteneur**

### 🔨 **Construire l’image Docker**

```sh
docker build -t student_api .
```

![2](https://github.com/user-attachments/assets/ee402eaa-c2c8-4b7d-9977-dc8170f2abf3)

### ▶️ **Lancer le conteneur**

```sh
docker run -d -p 5000:5000 student_api
```

![3](https://github.com/user-attachments/assets/54b8f933-878d-4b53-9bd9-0f14ad36c7b1)

---

## 📺 **Interface graphique du conteneur Docker**

> Visualisation de l’interface Docker Desktop.
![azb](https://github.com/user-attachments/assets/1729fd02-551a-49d3-96f4-ea79977028b3)

---

## 🏗️ **Test de l’API**


### 📜 **Vérifier les logs du conteneur**

```sh
docker logs <ID_du_conteneur>
```

![4](https://github.com/user-attachments/assets/21a283c4-537d-4568-b2a1-2fdbef990dfc)

### 🔍 **Effectuer une requête GET sur l’API**

```sh
curl -u root:root -X GET http://localhost:5000/supmit/api/v1.0/get_student_ages
```

![5](https://github.com/user-attachments/assets/b7c9085a-9c75-4843-9c19-a205db2e6e2f)

```sh
curl -u root:root -X GET http://localhost:5000/supmit/api/v1.0/get_student_ages/<student_name>
```
![6](https://github.com/user-attachments/assets/8133ed1b-6713-4356-9779-f87fedefbed2)
---

 ## Prérequis

- Un compte AWS avec les permissions nécessaires pour créer et gérer des instances EC2.
- Un compte Docker Hub pour stocker les images Docker.
- Jenkins installé et configuré avec les plugins nécessaires (Docker, Git, SSH, etc.).
- Git pour la gestion du code source.
- Une instance EC2 Ubuntu configurée avec Docker.

## Structure du Projet

- **`website/`** : Contient les fichiers de l'application frontend.
- **`simple_api/`** : Contient les fichiers de l'application backend.
- **`Dockerfile`** : Fichier de configuration pour la construction des images Docker.
- **`Jenkinsfile`** : Script définissant les étapes du pipeline CI/CD.
- **`student_age.json`** : Fichier de données utilisé par l'application backend.

## Étapes du Pipeline CI/CD

### 1. Intégration Continue (CI)

- **Clone du dépôt** : Récupération du code source depuis le dépôt Git.
- **Build des images Docker** : Construction des images Docker pour le frontend et le backend.
- **Tests** : Vérification du bon fonctionnement des images Docker.
- **Release** : Envoi des images Docker sur Docker Hub.

### 2. Déploiement Continu (CD)

- **Déploiement sur AWS EC2** : 
  - Connexion à l'instance EC2.
  - Récupération des images Docker depuis Docker Hub.
  - Arrêt et suppression des conteneurs existants.
  - Démarrage des nouveaux conteneurs avec les images mises à jour.
  - Copie des fichiers de données nécessaires.

## Configuration Jenkins

### Variables d'environnement

- **`DOCKER_REGISTRY`** : Registre Docker (par défaut `docker.io`).
- **`DOCKER_IMAGE_FRONTEND`** et **`DOCKER_IMAGE_BACKEND`** : Noms des images Docker.
- **`AWS_EC2_INSTANCE`** : Adresse de l'instance EC2.
- **`EC2_PRIVATE_KEY`** : Clé SSH pour se connecter à l'instance EC2 (stockée dans les credentials Jenkins).

### Credentials Jenkins

- **`dockerhub-creds`** : Identifiants Docker Hub (username et password).
- **`AWS_SSH_CREDENTIAL`** : Clé privée SSH pour l'accès à l'instance EC2.

## Déploiement Automatisé

Le pipeline Jenkins exécute les étapes suivantes :

1. Clone le dépôt Git.
2. Construit les images Docker pour le frontend et le backend.
3. Pousse les images sur Docker Hub.
4. Se connecte à l'instance EC2 et déploie les conteneurs Docker.