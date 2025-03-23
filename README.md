# Devops_RACHCHAD_Ouadie-RACHDI_Anouar-ABDELHADI_Salah
🌌 Conception et Déploiement d’un Système de Gestion des Âges Étudiants avec Docker et Flask API : Une Fusion Élégante de Technologie et d’Art
🌟 Introduction
1.1 L’Essence du Projet
Plongez dans un projet innovant qui allie esthétique et fonctionnalité : un Système de Gestion des Âges des Étudiants conçu avec Flask API, PHP, et conteneurisé grâce à Docker. Ce système offre une expérience fluide pour récupérer et afficher les âges des étudiants via une API RESTful, le tout dans une interface web dynamique et visuellement captivante.

1.2 Les Piliers Technologiques
Flask (Python) 🐍 : Le cœur de l’API RESTful, orchestrant la gestion des données d’âge avec élégance.

PHP 🔧 : L’artisan de l’interface web, transformant les données en une expérience visuelle immersive.

Docker 🐳 : Le maître d’œuvre, encapsulant chaque composant dans des conteneurs pour un déploiement harmonieux.

Docker Compose 🔄 : Le chef d’orchestre, synchronisant les services pour une performance sans faille.

1.3 L’Art du Déploiement
L’application est déployée avec Docker, où Flask et PHP coexistent dans des conteneurs distincts, communiquant via un réseau en pont Docker. Cette architecture modulaire et évolutive est un véritable chef-d’œuvre de modernité.

🏛️ Architecture du Système : Une Symphonie Technologique
2.1 Vision Globale
Le système repose sur une architecture client-serveur :

Le frontend PHP dialogue avec l’API Flask pour récupérer les données.

L’API Flask puise les informations d’âge des étudiants dans un fichier JSON.

Les deux services, encapsulés dans des conteneurs Docker, interagissent harmonieusement via un réseau partagé.

2.2 Les Composants Clés
API Flask (student_age.py) 🌐
