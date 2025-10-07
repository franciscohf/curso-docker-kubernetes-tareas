# Clase 2 - Dockerización de Mi Aplicación

## Aplicación

**Lenguaje:** JAVA
**Framework:** Spring boot
**Descripción:** API REST para ordenes de productos

**Endpoints:**
- GET /producto - listar productos
- GET /orden - listar ordenes
- POST /producto - Crear producto

## Dockerfile

\`\`\`dockerfile
# Stage 1: Build
# Fase de compilación con imagen ligera de OpenJDK 21
FROM openjdk:21-slim AS builder

# Crea un grupo y usuario no root
RUN addgroup --gid 1002 appgroup && useradd --uid 1002 -g appgroup -s /bin/bash appuser

# Establece el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copia el archivo de definición de dependencias
COPY pom.xml .


# Ejecuta para Maven
RUN apt-get update && apt-get install -y maven


# Copia el código fuente
COPY src ./src

# Compila y empaqueta la aplicación en un JAR ejecutable
#RUN mvn package -DskipTests

RUN mvn clean install -DskipTests

# Stage 2: Runtime
# Etapa 2: Fase de ejecución (Runtime)
# Usa una imagen de JRE ligera con OpenJDK 21 para el runtime
FROM eclipse-temurin:21-jre-jammy

WORKDIR /app

# Copia el JAR desde la fase de compilación
COPY --from=builder /app/target/*.jar ./*.jar


# Cambia al usuario no root antes de ejecutar tu aplicación
USER appuser

# Expone el puerto que tu aplicación Spring Boot utiliza (por defecto 8080)
EXPOSE 8080

# Define el comando para ejecutar la aplicación en el contenedor
ENTRYPOINT ["java", "-jar", "*.jar"]

**Explicación:**

| Stage | Propósito |
|-------|-----------|
| builder  | compilación con imagen ligera de OpenJDK 21 |
| FROM eclipse-temurin:21-jre-jammy | Establece la fase de Runtime|


## Build

\`\`\`bash
docker build -t spring-boot-docker:v1.0 .
\`\`\`

**Salida:**
\`\`\`
[+] Building 5.3s (18/18) FINISHED
=> => naming to docker.io/library/spring-boot-docker:v1.0
 => => unpacking to docker.io/library/spring-boot-docker:v1.0
\`\`\`

**Tamaño final:** 505MB

## Testing

![Docker Images](screenshots/docker-images.png)
![Container Running](screenshots/docker-ps.png)
![API Response](screenshots/endpoints.png)

## Docker Hub

**URL:** https://hub.docker.com/repository/docker/francisco13/spring-boot-api

![Docker Hub](screenshots/dockerhub.png)

## Optimizaciones

- Usuario non-root (appuser)
- .dockerignore 
.git/
.gitignore
target/
.idea/

## Conclusiones

Aprendí a crear el dockerfile