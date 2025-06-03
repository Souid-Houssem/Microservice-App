FROM openjdk:17-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy JAR file into container
COPY target/gateway-0.0.1-SNAPSHOT.jar /app/gateway.jar

# Set the command to run the service
CMD ["java", "-jar", "/app/gateway.jar"]

# Expose the port used by the gateway (typically 8888 or 8080)
EXPOSE 8888
