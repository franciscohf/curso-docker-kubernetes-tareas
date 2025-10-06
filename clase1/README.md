# curso-docker-kubernetes-tareas
Curso de docker kubernetes

# MYSQL

docker run -d --name mi-mysql -e MYSQL_ROOT_PASSWORD==mi-password-seguro -p 3306:3306 mysql:latest

# Comandos de verificación

docker ps

docker ps -a

docker logs e9182078cf3c

# Comandos de limpieza

docker stop e9182078cf3c

docker rm e9182078cf3c

docker ps -a

# Explicación 

| flag | Descripción | 
|---|---|
| -d | se ejecuta en segundo plano |
| --name | nombre del contenedor |
| -e | variables de enterno |
| -p | mapeo del puerto |