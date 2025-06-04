FROM openjdk:17-alpine

# Créer un dossier pour l'application
RUN mkdir /app
WORKDIR /app

# Copier le fichier JAR généré par Maven dans le conteneur
COPY target/*.jar /app/analyse-service.jar

# Lancer le service
CMD ["java", "-jar", "/app/analyse-service.jar"]

# Exposer le port utilisé par le service (à adapter selon votre config)
EXPOSE 8090
