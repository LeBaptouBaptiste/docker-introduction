# --- Etape 1 : build ---
FROM node:22-alpine AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build            # produit /app/dist

# --- Etape 2 : uniquement les fichiers statiques, servis sans root ---
FROM nginxinc/nginx-unprivileged:1.31.7-alpine@sha256:b5047b9b76845eac124358373c6852377c52e4b05834a47647e955dd91cb8f1e
USER root
RUN apk del --no-cache curl nginx-module-xslt nginx-module-image-filter nginx-module-geoip nginx-module-njs
USER 101
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 8080