FROM eclipse-temurin:17-jdk-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy JAR file and rename
COPY target/*.jar /app/billing-service.jar

# Expose the port
EXPOSE 8083

# Run the service
CMD ["java", "-jar", "/app/billing-service.jar"]
