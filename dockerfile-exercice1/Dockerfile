# Utiliser une image de base Node.js légère
FROM node:18-alpine

# Définir le répertoire de travail de l'application
WORKDIR /app

# Copier les fichiers package.json et package-lock.json pour installer les dépendances
COPY package.json package-lock.json ./

# Copier les fichiers sources de l'application dans le conteneur
COPY public ./public
COPY src ./src

# Installer les dépendances, construire l'application et nettoyer les modules Node.js
RUN npm install
RUN npm install -g serve
RUN npm run build
RUN rm -rf node_modules

# Exposer le port
EXPOSE 3000

# Démarrer l'application 
CMD ["serve", "-s", "build", "-l", "3000"]