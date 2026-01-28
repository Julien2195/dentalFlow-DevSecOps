# ======================
# BUILD STAGE
# ======================
FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build   # juste next build, plus next export

# ======================
# RUNTIME STAGE
# ======================
FROM nginx:alpine

COPY --from=build /app/.next /usr/share/nginx/html/.next
COPY --from=build /app/public /usr/share/nginx/html/public
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
