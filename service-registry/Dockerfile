# Use a base image with JDK 17 and Maven installed
FROM maven:3.8.4-openjdk-17 AS build
# Set the working directory inside the container
WORKDIR /app

# Copy the Maven project descriptor files
COPY pom.xml .

# Copy the entire source code
COPY src ./src

# Build the application with Maven
RUN mvn clean package

# Use a lighter base image for the runtime environment
FROM openjdk:17-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the JAR file from the build stage to the runtime environment
COPY --from=build /app/target/*.jar /app/service.jar

EXPOSE 8761

# Specify the command to run your application
CMD ["java", "-jar", "/app/service.jar"]
