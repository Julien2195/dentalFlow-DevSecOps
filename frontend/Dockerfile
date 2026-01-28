# Étape 1 : Build React
FROM node:20-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm ci --production

COPY . .
RUN npm run build

# Étape 2 : Nginx minimal pour prod
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]