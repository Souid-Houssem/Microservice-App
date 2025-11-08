FROM eclipse-temurin:17-jdk-alpine

# Create and set working directory
WORKDIR /app

# Copy JAR file into container
COPY target/product-service-0.0.1-SNAPSHOT.jar product-service.jar

# Expose the microservice port
EXPOSE 8081

# Run the service
CMD ["java", "-jar", "product-service.jar"]
