FROM eclipse-temurin:17-jdk-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy JAR file into container
COPY target/gateway-0.0.1-SNAPSHOT.jar /app/gateway.jar

# Expose the port used by the gateway
EXPOSE 8888

# Run the gateway service
CMD ["java", "-jar", "/app/gateway.jar"]
