# Usa una imagen base ligera de OpenJDK
FROM openjdk:17-jdk-slim

# Define el archivo JAR como un argumento
ARG JAR_FILE=target/*.jar

# Copia el archivo JAR generado al contenedor
COPY ${JAR_FILE} app.jar

# Expone el puerto en el que la aplicación escucha
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "/app.jar"]
