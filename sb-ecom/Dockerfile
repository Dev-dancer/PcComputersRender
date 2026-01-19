# ========================
# Stage 1: Build the application
# ========================
FROM maven:3.9.9-eclipse-temurin-21 AS build

WORKDIR /app

# Copy pom.xml and download dependencies first
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source code and build
COPY src ./src
RUN mvn clean package -DskipTests

# ========================
# Stage 2: Run the application
# ========================
FROM eclipse-temurin:21-jre

WORKDIR /app

# Copy the built JAR from the build stage
COPY --from=build /app/target/sb-ecom-0.0.1-SNAPSHOT.jar app.jar

# Expose the application port
EXPOSE 8080

# Run the Spring Boot application
ENTRYPOINT ["java", "-jar", "app.jar"]
