FROM openjdk:17-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy JAR file and rename
COPY target/*.jar /app/billing-service.jar

# Set the command to run the service
CMD ["java", "-jar", "/app/billing-service.jar"]

# Expose the port
EXPOSE 8083
