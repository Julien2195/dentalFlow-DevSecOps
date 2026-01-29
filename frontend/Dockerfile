# ======================
# BUILD STAGE
# ======================
FROM node:25-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build   # juste next build, plus next export

# ======================
# RUNTIME STAGE
# ======================
FROM nginx:alpine

# Next.js "output: export" generates a fully static site in /app/out
COPY --from=build /app/out /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
