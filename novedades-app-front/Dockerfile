# Etapa de build: usa Node.js y Yarn para compilar la aplicación React
FROM node:16-alpine as build

WORKDIR /app

# Copia el package.json y yarn.lock
COPY package.json yarn.lock ./

# Instala las dependencias usando Yarn
RUN yarn install --frozen-lockfile

# Copia el resto del código fuente y compila la aplicación
COPY . .
RUN yarn build

# Etapa final: usa Nginx para servir la aplicación compilada
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
