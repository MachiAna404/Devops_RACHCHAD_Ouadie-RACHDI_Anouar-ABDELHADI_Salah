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

# 📌 **Étape 2 : Infrastructure as Code**


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

# 📌 **Étape 3 : Docker Registry**

À cette étape, nous allons configurer un registre Docker privé. Un registre privé est un espace de stockage sécurisé où vous pouvez héberger et gérer vos images Docker localement, sans avoir à utiliser un service externe comme Docker Hub. Une fois le registre configuré, vous pourrez y pousser (envoyer) vos images Docker et les récupérer facilement. De plus, vous pourrez gérer ce registre à travers une interface web, ce qui facilitera l'administration et l'accès aux images stockées.

L'étape suivante consiste donc à démarrer ce registre privé Docker sur votre machine.


## 📜 **Un registre Docker**

Nous avons démarré un registre privé local pour stocker nos images Docker en utilisant la commande suivante :


`docker run -d -p 5001:5000 --name registry registry:2`
Voici ce que chaque partie de cette commande fait :

docker run: Lance un nouveau conteneur Docker.

**-d:** Démarre le conteneur en arrière-plan (mode détaché).

**-p 5001:5000:** Mappe le port 5000 du conteneur (port par défaut du registre Docker) au port 5001 de votre machine locale. Cela permet d’accéder au registre via localhost:5001.

**--name registry:** Attribue un nom au conteneur, ici "registry", afin de pouvoir l'identifier facilement.

**registry:2:** Utilise l'image officielle registry version 2 pour créer le registre privé.
![3](https://github.com/user-attachments/assets/6552b4de-a14a-4a56-9b7b-280e12bab228)
# Explication des composants

## 🗂️ Service Registry
- **Image** : Utilise l'image officielle `registry:2`
- **Port** : Exposé sur le port 5001 de l'hôte (pour éviter les conflits avec l'API sur le port 5000)
- **Volume** : Utilise un volume nommé `registry-data` pour persister les images stockées
- **Redémarrage** : Configuré pour toujours redémarrer en cas d'échec

## 🖥️ Service Registry UI
- **Image** : Utilise l'image `joxit/docker-registry-ui` pour fournir une interface graphique
- **Port** : Interface web accessible sur le port 8080
- **Environnement** : Configure le titre et l'URL du registre
- **Dépendances** : Démarre seulement après le démarrage du registre

## 🌐 Réseau et Volume
- **Réseau** : Un réseau dédié `registry-network` pour isoler la communication
- **Volume** : Un volume `registry-data` pour assurer la persistance des données
![2](https://github.com/user-attachments/assets/f8c81c17-1465-491d-beb7-6d1a1f21db63)

### ✅ **Objectif**

Nous avons vérifié si le registre privé fonctionne bien avec : _ Tagger l’image et l’envoyer au registre privé docker push localhost:5001/student_api

Nous avons vérifié que le registre privé fonctionne correctement en taguant une image Docker et en l'envoyant vers ce registre privé avec la commande suivante :


`docker push localhost:5001/student_api`
Voici ce que fait chaque étape :

Tagger l'image : Avant de pousser une image vers le registre privé, nous devons d'abord la taguer avec l'adresse de notre registre local. Par exemple, pour l'image student_api, nous utilisons la commande suivante pour la taguer :


`docker tag student_api localhost:5001/student_api`
Cela associe l'image student_api au registre privé qui tourne sur localhost:5001.

Envoyer l'image au registre privé : Ensuite, nous utilisons la commande docker push pour envoyer l'image taggée vers le registre privé. Cette commande pousse l'image vers localhost:5001/student_api, qui est notre registre local.

Cela permet de vérifier que le registre fonctionne correctement et que vous pouvez envoyer (push) vos images Docker dedans pour les stocker et les utiliser plus tard.
![6](https://github.com/user-attachments/assets/c5015693-fe8d-4dda-a762-eac1d1ade1e6)
![7](https://github.com/user-attachments/assets/358a3475-0847-4084-bf9e-09ce12c4c494)


## 📺 **Une interface web pour voir l'image poussée en tant que conteneur.**

Nous avons lancé une interface web pour gérer les images Docker en utilisant l'image joxit/docker-registry-ui. Cette interface permet de visualiser et de gérer les images stockées dans notre registre privé Docker via un navigateur, facilitant ainsi l'administration des images directement depuis une interface graphique accessible localement.
![Image 6](https://github.com/user-attachments/assets/d1545a63-cd36-4e60-9019-ba2cd6250720)
![Image 5](https://github.com/user-attachments/assets/5a78cd58-b7de-4119-8129-d904b657f5dc)




# Déploiement Automatisé d'une Application Web avec CI/CD sur Jenkins et AWS

## 📋 Description du Projet
Ce projet implémente un pipeline CI/CD complet pour déployer une application web (frontend + backend) sur AWS EC2 en utilisant Jenkins. Le processus inclut la construction d'images Docker, leur publication sur Docker Hub, et le déploiement automatisé sur une instance EC2 avec gestion des données.

---

## 🛠 Prérequis Techniques

### Comptes et Services
- **AWS Account**  
  Permissions nécessaires :  
  ✅ EC2 Full Access  
  ✅ VPC/Subnet Configuration  
  🔑 Clé SSH enregistrée dans IAM

- **Docker Hub**  
  Compte avec dépôt créé pour :  
  - `salah/frontend`  
  - `salah/backend`

- **Jenkins Server**  
  Plugins installés :  
  - Docker Pipeline  
  - Git  
  - SSH Agent  
  - Credentials Binding

### Infrastructure
- **Instance EC2**  
  - OS : Ubuntu 22.04 LTS  
  - Configuration minimale : t2.micro  
  - Ports ouverts : 80 (HTTP), 5000 (Backend)  
  - Docker Engine installé

---

## 📂 Structure du Projet

├── website/ # Frontend (fichiers statiques)
│ ├── index.html
│ └── ...
├── simple_api/ # Backend (API Python/Node)
│ ├── app.py
│ └── student_age.json # Fichier de données
├── Dockerfile # Config Docker pour chaque service
└── Jenkinsfile # Pipeline CI/CD


---

## 🔄 Pipeline CI/CD - Explication Détaillée

### 1. **Intégration Continue (CI)**
#### 🔹 Clone du Dépôt
```groovy
git branch: 'main', 
url: 'https://github.com/MachiAna404/Devops_RACHCHAD_Ouadie-RACHDI_Anouar-ABDELHADI_Salah.git'

Récupère le code depuis la branche main

🔹 Build des Images Docker (Parallélisé)
parallel {
    stage('Frontend') {
        sh 'docker build -t salah/frontend:1.0 ./website'
    }
    stage('Backend') {
        sh 'docker build -t salah/backend:1.0 ./simple_api'
    }
}

Construit 2 images séparées avec tags versionnés

Chaque image inclut :

Frontend : Serveur Nginx + fichiers statiques

Backend : Runtime Python/Node + dépendances

🔹 Push vers Docker Hub

withCredentials([usernamePassword(...)]) {
    sh 'docker login -u $DOCKER_USER'
    sh 'docker push salah/frontend:1.0'
    sh 'docker push salah/backend:1.0'
}

Utilise des credentials sécurisés stockés dans Jenkins

Publie les images dans le registry Docker Hub

2. Déploiement Continu (CD)
🔸 Déploiement sur EC2

scp -i $EC2_PRIVATE_KEY student_age.json ec2-user@IP:/home/ec2-user/
ssh -i $EC2_PRIVATE_KEY ec2-user@IP '
    docker login -u $DOCKER_USERNAME
    docker pull salah/frontend:1.0
    docker pull salah/backend:1.0
    docker stop frontend backend || true
    docker run -d -p 5000:5000 -v /data --name backend salah/backend:1.0
    docker run -d -p 80:80 --name frontend salah/frontend:1.0
    docker cp student_age.json backend:/data
'
Étapes clés :

Copie du fichier JSON via SCP

Connexion SSH sécurisée

Mise à jour des conteneurs avec zero-downtime

Montage de volume pour persistance des données

⚙ Configuration Jenkins
Variables d Environnement
Variable	Valeur	Description
DOCKER_REGISTRY	docker.io	Registry Docker
AWS_EC2_INSTANCE	ec2-user@IP	User + IP EC2
EC2_PRIVATE_KEY	credentials()	Clé SSH chiffrée
Credentials
Docker Hub

ID : dockerhub-creds

Stocke : username + password

AWS SSH Key

ID : AWS_SSH_CREDENTIAL

Format : Clé privée PEM

Étapes clés :

Copie du fichier JSON via SCP

Connexion SSH sécurisée

Mise à jour des conteneurs avec zero-downtime

Montage de volume pour persistance des données

⚙ Configuration Jenkins
Variables d Environnement
Variable	Valeur	Description
DOCKER_REGISTRY	docker.io	Registry Docker
AWS_EC2_INSTANCE	ec2-user@IP	User + IP EC2
EC2_PRIVATE_KEY	credentials()	Clé SSH chiffrée
Credentials
Docker Hub

ID : dockerhub-creds

Stocke : username + password

AWS SSH Key

ID : AWS_SSH_CREDENTIAL

Format : Clé privée PEM