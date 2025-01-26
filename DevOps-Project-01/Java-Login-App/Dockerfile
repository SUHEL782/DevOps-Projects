# Use the Maven official image as the base image
FROM maven:3.8.3-openjdk-17 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the project files into the container
COPY . .

# Build the project and skip tests
RUN mvn clean package -DskipTests

# Use an OpenJDK runtime image to run the built application
FROM openjdk:17-jdk-slim

# Set the working directory for the application runtime
WORKDIR /app

# Copy the built WAR file from the Maven build stage
COPY --from=build /app/target/dptweb-1.0.war /app/dptweb.war

# Expose the port on which the application will run
EXPOSE 8080

# Set the default command to run the application
CMD ["java", "-jar", "/app/dptweb.war"]
