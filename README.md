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

### 📌 **Étape 1 : Construire et Tester l'API**

Dans cette section, nous allons construire et tester notre API Flask en suivant plusieurs étapes.

---

### ✅ **Objectif**

Nous avons utilisé l’image `python:3.8-buster` comme base pour notre conteneur Docker.
Nous avons également ajouté des métadonnées avec `LABEL maintainer` pour indiquer les informations du responsable de l’image Docker.

![1](https://github.com/user-attachments/assets/8241d778-6338-4552-8061-0784ea1cb1a2)

---

## 📜 **Explication du Dockerfile**

Le fichier `Dockerfile` permet de construire une image Docker pour notre API Python (probablement basée sur Flask). Voici une explication détaillée ligne par ligne :

### 🏗️ **1. Utiliser une image de base Python 3.8**

```dockerfile
FROM python:3.8-buster
```

- `FROM` définit l’image de base utilisée pour construire l’image Docker.
- Ici, on utilise `python:3.8-buster`, qui est une version officielle de Python 3.8 basée sur Debian Buster.

### 👤 **2. Ajouter des métadonnées (mainteneur)**

```dockerfile
LABEL maintainer="Abdelhadi_Rachdi_Rachchad <Rachchad_Rachdi_Abdelhadi@gmail.com>"
```

- `LABEL` permet d’ajouter des métadonnées.
- Ici, il spécifie le mainteneur avec son nom et son email.

### 📂 **3. Définir le répertoire de travail**

```dockerfile
WORKDIR /app
```

- `WORKDIR` définit `/app` comme répertoire de travail dans le conteneur.
- Toutes les commandes suivantes (comme `COPY` et `RUN`) seront exécutées à partir de ce répertoire.

### 🔧 **4. Installer les dépendances système**

```dockerfile
RUN apt update -y && apt install -y \
    python3-dev \
    libsasl2-dev \
    libldap2-dev \
    libssl-dev
```

- `RUN` exécute des commandes dans le conteneur pendant la construction.
- On met à jour les paquets (`apt update -y`) et installe des bibliothèques essentielles (`apt install -y`).

### 📜 **5. Copier et installer les dépendances Python**

```dockerfile
COPY requirements.txt .
RUN pip3 install -r requirements.txt
```

- `COPY requirements.txt .` : copie le fichier `requirements.txt` dans le conteneur.
- `RUN pip3 install -r requirements.txt` : installe les dépendances Python nécessaires.

### 📝 **6. Copier le code source**

```dockerfile
COPY student_age.py .
```

- `COPY student_age.py .` : copie le fichier principal de l'API dans le répertoire `/app` du conteneur.

### 📁 **7. Créer un dossier pour les données persistantes**

```dockerfile
VOLUME /data
```

- `VOLUME` définit `/data` comme un répertoire persistant.

### 🌐 **8. Exposer le port 5000**

```dockerfile
EXPOSE 5000
```

- `EXPOSE 5000` : ouvre le port 5000 pour accéder à l’API Flask.

### 🚀 **9. Lancer l’API Flask**

```dockerfile
CMD ["python3", "./student_age.py"]
```

- `CMD` définit la commande par défaut du conteneur.
- Ici, il lance `student_age.py` avec Python.

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











---

### 📌 **Étape 2 : Infrastructure as Code**


Dans cette étape, nous allons automatiser le déploiement de l’API et du site web PHP en utilisant **Docker Compose**. Création du fichier `docker-compose.yml`
### ✅ **Objectif**
Supprimez le conteneur que vous avez créé précédemment.
![b](https://github.com/user-attachments/assets/cae77799-e900-4e3a-8766-a38ab56ccd26)

### ✅ **Objectif**
Nous avons créé le fichier `docker-compose.yml` qui définit les services API et Website.

![1](https://github.com/user-attachments/assets/72be0063-0dfc-4a7c-bb69-dc91393b0d87)

### ✅ **Objectif**
Nous avons lancé l’application en une seule commande : `docker-compose up --build -d`

![c](https://github.com/user-attachments/assets/59eb2050-0592-4867-a43e-b67bcfef273a)


---

### Tester l’application

### ✅ **Objectif**

Nous avons accédé au site web via [http://localhost:8080](http://localhost:8080) et cliqué sur "List Student" pour vérifier que l’API fonctionne.

![WhatsApp Image 2025-03-23 at 6 33 44 PM](https://github.com/user-attachments/assets/1e0f7b89-6604-4853-b9ba-8096cb4c8bd3)

Apres on clique sur le bouttons : "List Student"

![4 ](https://github.com/user-attachments/assets/6f9b0c73-e79f-42ac-982c-13b64eacad2a)


---

### 📌 **Étape 3**


À cette étape, nous allons configurer un registre Docker privé. Un registre privé est un espace de stockage sécurisé où vous pouvez héberger et gérer vos images Docker localement, sans avoir à utiliser un service externe comme Docker Hub. Une fois le registre configuré, vous pourrez y pousser (envoyer) vos images Docker et les récupérer facilement. De plus, vous pourrez gérer ce registre à travers une interface web, ce qui facilitera l'administration et l'accès aux images stockées.

L'étape suivante consiste donc à démarrer ce registre privé Docker sur votre machine.
### ✅ **Objectif**

Nous avons démarré un registre privé local pour stocker nos images Docker. docker run -d -p 5001:5000 --name registry registry:2

Nous avons démarré un registre privé local pour stocker nos images Docker en utilisant la commande suivante :


`docker run -d -p 5001:5000 --name registry registry:2`
Voici ce que chaque partie de cette commande fait :

-**-docker run:** Lance un nouveau conteneur Docker.

**-d:** Démarre le conteneur en arrière-plan (mode détaché).

-**-p 5001:5000:** Mappe le port 5000 du conteneur (port par défaut du registre Docker) au port 5001 de votre machine locale. Cela permet d’accéder au registre via localhost:5001.

-**--name registry:** Attribue un nom au conteneur, ici "registry", afin de pouvoir l'identifier facilement.

-**-registry:2:** Utilise l'image officielle registry version 2 pour créer le registre privé.
![3](https://github.com/user-attachments/assets/6552b4de-a14a-4a56-9b7b-280e12bab228)
![1](https://github.com/user-attachments/assets/09ffd38d-6450-44ff-8d7e-b45ae85feff9)

Capture d'écran 2025-03-21 125124
✅ Objectif :

Nous avons vérifié si le registre privé fonctionne bien avec : _ Tagger l’image et l’envoyer au registre privé docker push localhost:5001/student_api
![6](https://github.com/user-attachments/assets/c5015693-fe8d-4dda-a762-eac1d1ade1e6)
![7](https://github.com/user-attachments/assets/358a3475-0847-4084-bf9e-09ce12c4c494)

✅ Objectif :

Nous avons lancé une interface web pour gérer les images Docker avec :
![Image 6](https://github.com/user-attachments/assets/d1545a63-cd36-4e60-9019-ba2cd6250720)
![Image 5](https://github.com/user-attachments/assets/5a78cd58-b7de-4119-8129-d904b657f5dc)



kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkk
![2](https://github.com/user-attachments/assets/f8c81c17-1465-491d-beb7-6d1a1f21db63)
![3](https://github.com/user-attachments/assets/6552b4de-a14a-4a56-9b7b-280e12bab228)
![4](https://github.com/user-attachments/assets/e898b1bb-bbae-453a-b82d-17e43235c63c)
![5](https://github.com/user-attachments/assets/a5a1ca32-7435-4382-81e0-7d03a9d65d62)
![6](https://github.com/user-attachments/assets/c5015693-fe8d-4dda-a762-eac1d1ade1e6)
![7](https://github.com/user-attachments/assets/358a3475-0847-4084-bf9e-09ce12c4c494)
![8](https://github.com/user-attachments/assets/b4b141f4-9aa3-45d6-b856-6725185db58b)

![9](https://github.com/user-attachments/assets/350116e1-f3dd-4c04-998c-5d07ff7f9575)

![10](https://github.com/user-attachments/assets/9cf3d2a4-2a68-4200-88ac-9a7140cbde52)











