# Étape 1 : Build Maven
FROM maven:3.9.2-eclipse-temurin-20 AS build
WORKDIR /app

# Copier les pom.xml et modules
COPY ../pom.xml ./pom.xml
COPY ../dentaflow-core ./dentaflow-core
COPY ../dentaflow-client ./dentaflow-client
COPY ../dentaflow-app ./dentaflow-app

# Build jar (skip tests)
RUN mvn clean package -DskipTests

# Étape 2 : Runtime minimal
FROM eclipse-temurin:25-jre-alpine
WORKDIR /app

# Ajouter CA certs et timezone
RUN apk add --no-cache ca-certificates tzdata \
    && cp /usr/share/zoneinfo/Europe/Paris /etc/localtime \
    && echo "Europe/Paris" > /etc/timezone \
    && apk del tzdata

# Copier le jar
COPY --from=build /app/dentaflow-app/target/dentaflow-app.jar ./dentaflow-app.jar

# Exposer port
EXPOSE 8080

# Lancer l'application
ENTRYPOINT ["java", "-jar", "dentaflow-app.jar"]