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

Explication du cockerfile : 
Le fichier Dockerfile que tu partages sert à construire une image Docker pour une application Python (dans ce cas, probablement une API utilisant Flask). Voici une explication détaillée de chaque ligne :

1. Utiliser l'image de base Python 3.8

`FROM python:3.8-buster`
 
FROM indique l’image de base à utiliser pour construire cette image Docker.

Ici, l’image utilisée est python:3.8-buster, qui est une version officielle de Python 3.8 basée sur Debian Buster. Cela permet d’avoir une version stable de Python dans un environnement Debian.

2. Spécifier les informations du mainteneur

`LABEL maintainer="Abdelhadi_Rachdi_Rachchad <Rachchad_Rachdi_Abdelhadi@gmail.com>"`
LABEL est utilisé pour ajouter des métadonnées à l’image Docker.

Dans ce cas, il spécifie le mainteneur de l’image Docker avec son nom et son adresse e-mail. Cela aide à identifier qui a créé ou maintient l’image.

3. Définir le répertoire de travail dans le conteneur
`WORKDIR /app`
WORKDIR définit le répertoire de travail à l'intérieur du conteneur.

Ici, le répertoire /app est créé (s'il n'existe pas déjà) et toute commande suivante (comme COPY ou RUN) sera exécutée à partir de ce répertoire.

4. Installer les dépendances système nécessaires

```RUN apt update -y && apt install -y \
    python3-dev \
    libsasl2-dev \
    libldap2-dev \
    libssl-dev```
RUN exécute des commandes dans le conteneur pendant la construction de l'image.

Ici, apt update -y met à jour les informations des paquets disponibles, et apt install -y installe des paquets système nécessaires :

python3-dev : fichiers de développement pour Python 3 (utile pour compiler des extensions).

libsasl2-dev, libldap2-dev, libssl-dev : bibliothèques de développement pour des fonctionnalités supplémentaires comme l’authentification SASL, LDAP, et SSL, probablement nécessaires pour certaines bibliothèques Python.

5. Copier le fichier des dépendances Python dans le conteneur

`COPY requirements.txt .`
COPY copie des fichiers depuis le répertoire local (dans le même répertoire que le Dockerfile) vers le conteneur.

Ici, requirements.txt, qui contient la liste des dépendances Python nécessaires, est copié dans le répertoire de travail du conteneur (/app).

6. Installer les dépendances Python

`RUN pip3 install -r requirements.txt`

RUN pip3 install -r requirements.txt installe les dépendances Python spécifiées dans le fichier requirements.txt.

Ce fichier contient généralement des bibliothèques comme Flask, Django, ou d'autres, qui seront installées dans l'environnement Python du conteneur.

7. Copier le code source de l'API dans le conteneur

`COPY student_age.py .`
COPY student_age.py . copie le fichier Python student_age.py dans le répertoire de travail du conteneur (/app).

Ce fichier est probablement l’application principale qui définit ton API Flask.

8. Créer un dossier pour les données persistantes

`VOLUME /data`
VOLUME crée un point de montage pour un volume dans le conteneur.

Ici, /data est défini comme un volume pour stocker des données persistantes. Cela permet de conserver les données même si le conteneur est supprimé, en les associant à un volume externe.

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





