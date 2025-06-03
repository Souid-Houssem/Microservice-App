FROM openjdk:17-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy the JAR file into the container
COPY target/eureka-service-0.0.1-SNAPSHOT.jar /app/eureka-service.jar

# Run the Eureka service
CMD ["java", "-jar", "/app/eureka-service.jar"]

# Expose the port used by Eureka (typically 8761)
EXPOSE 8761
