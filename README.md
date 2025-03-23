# 🌌 **Conception et Déploiement d’un Système de Gestion des Âges Étudiants avec Docker et Flask API : Une Fusion Élégante de Technologie et d’Art**

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

## 🛠️ **Structure**
##📌  **Étape I  ** Construire et tester l'API

Dans cette partie, nous allons construire et tester l’API Flask en suivant plusieurs étapes.

##✅  **Objectif  **

Nous avons utilisé l’image python:3.8-buster comme base pour notre conteneur. Ajout des informations du mainteneur Nous avons ajouté notre nom et email dans le Dockerfile avec LABEL maintainer.

![1](https://github.com/user-attachments/assets/8241d778-6338-4552-8061-0784ea1cb1a2)

✅ Objectif :

Nous avons configuré le conteneur pour exposer le port 5000 afin d’accéder à l’API Flask. Construction et lancement de l’image Docker Nous avons construit l’image avec la commande : docker build -t student_api .

![2](https://github.com/user-attachments/assets/ee402eaa-c2c8-4b7d-9977-dc8170f2abf3)



Puis, nous avons lancé un conteneur avec cette commande :

![3](https://github.com/user-attachments/assets/54b8f933-878d-4b53-9bd9-0f14ad36c7b1)

pour l interface graphique 
( hna photo dial docker env ) 






