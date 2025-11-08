FROM eclipse-temurin:17-jdk-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy the JAR file into the container
COPY target/Billing-producer-0.0.1-SNAPSHOT.jar /app/billing-producer.jar

# Expose the port used by the billing-producer service
EXPOSE 8088

# Run the billing-producer service
CMD ["java", "-jar", "/app/billing-producer.jar"]
