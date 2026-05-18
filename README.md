# Backend Ventas - Innovatech Chile

API REST desarrollada en Spring Boot para gestión de ventas, desplegada en AWS EC2 mediante contenedor Docker y pipeline CI/CD con GitHub Actions.

## Tecnologías
- Java 17
- Spring Boot 3.4.4
- MySQL 8.0
- Docker (multi-stage build)
- GitHub Actions (CI/CD)

## Arquitectura
- EC2 privada (subnet-privada 10.0.2.0/24)
- Puerto: 8080
- Base de datos: MySQL en ec2-data (3306)

Este backend se despliega **junto con Despachos** en la misma EC2 privada mediante el `docker-compose.yml` del repositorio de despachos.

## Endpoints
- `GET /api/v1/ventas` - Obtener todas las ventas
- `GET /api/v1/ventas/{id}` - Obtener venta por ID
- `POST /api/v1/ventas` - Crear venta
- `PUT /api/v1/ventas/{id}` - Actualizar venta
- `DELETE /api/v1/ventas/{id}` - Eliminar venta

## Pipeline CI/CD
El pipeline se activa con push en la rama `deploy`:
1. Construye imagen Docker multi-stage
2. Publica imagen en Docker Hub

El despliegue en EC2 se realiza desde el repo de despachos, que ejecuta `docker-compose` y levanta ambos servicios.

## Variables de entorno
| Variable | Descripción |
|----------|-------------|
| DB_ENDPOINT | IP del servidor MySQL |
| DB_PORT | Puerto MySQL (3306) |
| DB_NAME | Nombre de la base de datos |
| DB_USERNAME | Usuario MySQL |
| DB_PASSWORD | Contraseña MySQL |

## Persistencia
La base de datos corre en la EC2 de datos usando un volumen Docker **named** montado en `/var/lib/mysql`, lo que permite mantener la informacion al reiniciar o recrear el contenedor.