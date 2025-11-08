FROM eclipse-temurin:17-jdk-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy the JAR file into the container
COPY target/eureka-service-0.0.1-SNAPSHOT.jar /app/eureka-service.jar

# Expose Eureka port
EXPOSE 8761

# Run the Eureka service
CMD ["java", "-jar", "/app/eureka-service.jar"]
