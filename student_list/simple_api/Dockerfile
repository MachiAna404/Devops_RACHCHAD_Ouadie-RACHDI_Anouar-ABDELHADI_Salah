# Utiliser l'image de base Python 3.8
FROM python:3.8-slim-buster

# Définir le répertoire de travail dans le conteneur
WORKDIR /app

# Installer les dépendances système nécessaires
RUN apt-get update -y && apt-get install -y \
    python3-dev \
    libsasl2-dev \
    libldap2-dev \
    libssl-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Copier le fichier des dépendances Python
COPY requirements.txt .

# Installer les dépendances Python
RUN pip3 install --no-cache-dir -r requirements.txt

# Copier le code source de l'API
COPY student_age.py .

# Créer un dossier pour les données persistantes
VOLUME /data

# Exposer le port 5000 pour l'API
EXPOSE 5000

# Commande pour démarrer l'API
CMD ["python", "./student_age.py"]