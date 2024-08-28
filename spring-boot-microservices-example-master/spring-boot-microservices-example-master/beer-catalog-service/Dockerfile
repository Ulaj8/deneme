# Use an official Maven image to build the application
FROM maven:3.8.4-openjdk-11 AS build
WORKDIR /app

# Copy the pom.xml and install dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy the source code and build the application
COPY src ./src
RUN mvn package -DskipTests

# Use an official OpenJDK image to run the application
FROM openjdk:11-jre-slim
WORKDIR /app

# Copy the built jar file from the build stage
COPY --from=build /app/target/beer-catalog-service-*.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
