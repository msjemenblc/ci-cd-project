# Étape 1 : Construction de l'application
FROM maven:3.6.3-jdk-11-slim AS build

# Créer le répertoire de travail
RUN mkdir -p /workspace

# Définit le répertoire de travail dans l'image Docker
WORKDIR /workspace

# Copier les fichiers nécessaires pour Maven (pom.xml et src)
COPY back/pom.xml /workspace/pom.xml
COPY back/src /workspace/src

# Construire le projet avec Maven
RUN mvn -B -f pom.xml clean package -DskipTests

# Étape 2 : Créer l'image pour l'exécution
FROM openjdk:11-jdk-slim

# Copier le JAR généré depuis l'étape de construction
COPY --from=build /workspace/target/*.jar app.jar

# Exposer le port sur lequel l'application va tourner
EXPOSE 8080

# Définir l'entrypoint pour démarrer l'application
ENTRYPOINT ["java", "-jar", "app.jar"]
