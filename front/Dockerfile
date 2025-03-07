# Étape 1 : Construction du frontend
FROM node:latest AS build

# Créer le répertoire de travail pour l'application frontend
WORKDIR /usr/local/app

# Copier les fichiers nécessaires pour le frontend (package.json, etc.)
COPY front/package.json /usr/local/app/package.json
COPY front/package-lock.json /usr/local/app/package-lock.json
COPY front/ /usr/local/app/

# Installer les dépendances et construire l'application
RUN npm install
RUN npm run build

# Étape 2 : Préparer l'image de production avec Nginx
FROM nginx:latest AS production

# Copier la configuration Nginx (si tu en as une spécifique)
COPY front/nginx.conf /etc/nginx/conf.d/default.conf

# Copier le build du frontend dans le répertoire de Nginx pour servir l'application
COPY --from=build /usr/local/app/dist /usr/share/nginx/html

# Exposer le port sur lequel l'application va tourner
EXPOSE 80

# Lancer Nginx en mode non-démonisé
CMD ["nginx", "-g", "daemon off;"]
