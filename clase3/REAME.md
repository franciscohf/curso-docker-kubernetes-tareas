# Nombre de tu Aplicación

**Curso:** Docker & Kubernetes - Clase 3
**Estudiante:** Francisco H. Flores Huanca

Crea un servicio web con pagina estatitica, un mysql con su gestor adminer todos en el network app_network

## Stack

- **App:** Html
- **Base de datos:** MYSQL /
- **Gestor de datos:** ADMINER /

## Ejecución

1. Clonar:
   git clone https://github.com/tu-usuario/tu-repo.git
   cd curso-docker-kubernetes-tareas

2. Levantar servicios:
docker compose up -d



3. Acceder:

    API: http://localhost:3000



### 4. Cómo Probar

```markdown
## Verificación

1. Servicios corriendo:
   ```bash
   docker compose ps

Acceder a la web: http://localhost:XXXX

Verificar volumen persiste:

docker compose down
docker compose up -d
docker volume ls  # debe seguir existiendo

### 5. Capturas de Pantalla

```markdown
## Screenshots

### Servicios corriendo
![compose ps](screenshots/services.png)

### API funcionando
![API](screenshots/api.png)