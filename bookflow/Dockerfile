# Estágio 1: Build (Compilação)
# Usamos uma imagem que já contém o Maven e o JDK 17
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# 1. Copia apenas o arquivo de configuração de dependências
COPY pom.xml .

# 2. Baixa as dependências (isso acelera os próximos builds se você não mudar o pom.xml)
RUN mvn dependency:go-offline

# 3. Copia o código fonte
COPY src ./src

# 4. Gera o arquivo .jar (pulando os testes para o deploy ser mais rápido)
RUN mvn clean package -DskipTests

# Estágio 2: Runtime (Execução)
# Usamos uma imagem muito mais leve para rodar o app, apenas com o JRE
FROM openjdk:17-jdk-slim
WORKDIR /app

# Copia o JAR gerado no estágio anterior para a imagem final
# O uso de *.jar garante que ele encontre o arquivo independente da versão no pom.xml
COPY --from=build /app/target/*.jar app.jar

# Variável de porta que o Render exige
ENV PORT=8080
EXPOSE 8080

# Comando para iniciar a aplicação
ENTRYPOINT ["java", "-jar", "app.jar"]