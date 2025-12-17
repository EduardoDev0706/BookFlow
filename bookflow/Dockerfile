# Estágio de Build
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
# Copia todo o conteúdo da raiz para dentro do container
COPY . .
# Dá permissão de execução para o wrapper do maven e compila
RUN chmod +x mvnw && ./mvnw clean package -DskipTests

# Estágio de Execução
FROM openjdk:17-jdk-slim
WORKDIR /app
# Copia o jar gerado (o comando 'ls' ajuda a depurar se o nome mudar)
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]