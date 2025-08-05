FROM openjdk:17-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy JAR file into container
COPY target/*.jar /app/custmer-service.jar

# Set the command to run the service
CMD ["java", "-jar", "/app/custmer-service.jar"]

# Expose the same port as the microservice
EXPOSE 8082
 
