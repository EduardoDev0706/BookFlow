# Estágio 1: Build
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# Copia tudo para o container
COPY . .

RUN find . -name "mvnw" -exec chmod +x {} + && \
    (./mvnw clean package -DskipTests || (cd bookflow && ./mvnw clean package -DskipTests))

# Estágio 2: Runtime
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app

# Copia o JAR de onde quer que ele tenha sido gerado no estágio de build
COPY --from=build /app/**/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]