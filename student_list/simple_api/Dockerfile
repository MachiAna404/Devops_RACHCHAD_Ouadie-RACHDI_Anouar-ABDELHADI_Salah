# Utiliser l'image de base Python 3.8
FROM python:3.8-buster

# Spécifier les informations du mainteneur
LABEL maintainer="Abdelhadi_Rachdi_Rachchad <Rachchad_Rachdi_Abdelhadi@gmail.com>"

# Définir le répertoire de travail dans le conteneur
WORKDIR /app

# Installer les dépendances système nécessaires
RUN apt update -y && apt install -y \
    python3-dev \
    libsasl2-dev \
    libldap2-dev \
    libssl-dev

# Copier le fichier des dépendances Python dans le conteneur
COPY requirements.txt .

# Installer les dépendances Python
RUN pip3 install -r requirements.txt

# Copier le code source de l'API dans le conteneur
COPY student_age.py .

# Créer un dossier pour les données persistantes
VOLUME /data

# Exposer le port 5000 pour l'API Flask
EXPOSE 5000

# Commande pour démarrer l'API avec Flask
CMD ["python3", " student_age.py"]

