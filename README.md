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


![3](https://github.com/user-attachments/assets/fc685883-f960-4019-b39e-728212fd6054)


✅ Objectif : Nous avons testé l’API en appelant : curl -u root:root -X GET http://localhost:5000/supmit/api/v1.0/get_student_ages

![5](https://github.com/user-attachments/assets/b7c9085a-9c75-4843-9c19-a205db2e6e2f)

✅ Objectif :  Vérifiez les logs et assurez-vous que le conteneur écoute et est prêt à
répondre.

![6](https://github.com/user-attachments/assets/8133ed1b-6713-4356-9779-f87fedefbed2)













📌 Étape II : Infrastructure as Code

Dans cette étape, nous allons automatiser le déploiement de l’API et du site web PHP en utilisant Docker Compose. Création du fichier docker-compose.yml

✅ Objectif :

Nous avons créé le fichier docker-compose.yml qui définit les services API et Website.

![1](https://github.com/user-attachments/assets/72be0063-0dfc-4a7c-bb69-dc91393b0d87)

✅ Objectif : Nous avons lancé l’application en une seule commande : docker-compose up --build -d
![c](https://github.com/user-attachments/assets/59eb2050-0592-4867-a43e-b67bcfef273a)
![b](https://github.com/user-attachments/assets/cae77799-e900-4e3a-8766-a38ab56ccd26)


Tester l’application

✅ Objectif :

Nous avons accédé au site web via http://localhost:8080 et cliqué sur "List Student" pour vérifier que l’API fonctionne.

![4 ](https://github.com/user-attachments/assets/6f9b0c73-e79f-42ac-982c-13b64eacad2a)

##📌  **Étape III  **

![WhatsApp Image 2025-03-23 at 3 00 13 PM](https://github.com/user-attachments/assets/c6f41a0b-8830-47db-83c2-3a6bc1950c55)

![WhatsApp Image 2025-03-23 at 3 00 58 PM](https://github.com/user-attachments/assets/784c974e-79b3-4e8f-b554-5bd22fa6ecd4)


![WhatsApp Image 2025-03-23 at 3 01 35 PM](https://github.com/user-attachments/assets/39ecb75f-2189-470f-851b-dc62d2097729)



![WhatsApp Image 2025-03-23 at 3 10 44 PM](https://github.com/user-attachments/assets/feb1366d-997c-4fc6-ac37-d93e45f7418c)


![WhatsApp Image 2025-03-23 at 3 11 13 PM](https://github.com/user-attachments/assets/32737dc0-20dc-431b-9b60-ceb416a5f563)


![WhatsApp Image 2025-03-23 at 3 11 21 PM](https://github.com/user-attachments/assets/9199434f-188b-4623-958a-2ea723101bbf)

![WhatsApp Image 2025-03-23 at 3 11 54 PM](https://github.com/user-attachments/assets/98abcdd1-bfa3-4b6e-9fce-a7d2c3dfa96f)

![WhatsApp Image 2025-03-23 at 3 12 12 PM](https://github.com/user-attachments/assets/9dc8815a-1071-4416-9e07-aa9f2acd837d)


![WhatsApp Image 2025-03-23 at 3 12 59 PM](https://github.com/user-attachments/assets/a226dfe8-3db1-497b-b34f-580ac14294e6)


![WhatsApp Image 2025-03-23 at 3 13 46 PM](https://github.com/user-attachments/assets/2bee96f1-4271-4125-bd0c-400b2cf1c2a0)


