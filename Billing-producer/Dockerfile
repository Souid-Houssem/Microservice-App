FROM openjdk:17-alpine

# Create and set working directory
RUN mkdir /app
WORKDIR /app

# Copy the JAR file into the container
COPY target/Billing-producer-0.0.1-SNAPSHOT.jar /app/billing-producer.jar

# Run the billing-producer service
CMD ["java", "-jar", "/app/billing-producer.jar"]

# Expose the port used by the billing-producer service (update if needed)
EXPOSE 8088
