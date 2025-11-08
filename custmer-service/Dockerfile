FROM eclipse-temurin:17-jdk-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy JAR file into container
COPY target/*.jar /app/custmer-service.jar

# Expose the port used by the microservice
EXPOSE 8082

# Run the service
CMD ["java", "-jar", "/app/custmer-service.jar"]
