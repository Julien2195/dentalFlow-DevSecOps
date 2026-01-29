# ======================
# BUILD STAGE
# ======================
FROM maven:3.9.11-eclipse-temurin-25 AS build

WORKDIR /app

COPY pom.xml .
COPY dentaflow-core/ dentaflow-core/
COPY dentaflow-client/ dentaflow-client/
COPY dentaflow-app/ dentaflow-app/

RUN mvn dependency:go-offline

RUN mvn clean package -DskipTests

# ======================
# RUNTIME STAGE
# ======================
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

# Copier le JAR final du module dentaflow-app
COPY --from=build /app/dentaflow-app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]
