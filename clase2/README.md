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

RUN addgroup --gid 1002 appgroup && useradd --uid 1002 -g appgroup -s /bin/bash appuser

WORKDIR /app

COPY pom.xml .

RUN apt-get update && apt-get install -y maven

COPY src ./src

RUN mvn clean install -DskipTests


# Etapa 2: Fase de ejecución (Runtime)

FROM eclipse-temurin:21-jre-jammy

WORKDIR /app

COPY --from=builder /app/target/*.jar ./*.jar

USER appuser

EXPOSE 8080

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

![Docker Images](./screenshots/docker-images.png)

![Container Running](./screenshots/docker-ps.png)

![API Response](./screenshots/endpoints.png)

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