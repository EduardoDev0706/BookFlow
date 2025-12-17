# Estágio 1: Build
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY . .

RUN cd bookflow && chmod +x mvnw && ./mvnw clean package -DskipTests

# Estágio 2: Runtime
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app

COPY --from=build /app/bookflow/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]