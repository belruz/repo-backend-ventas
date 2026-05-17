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
- IP privada: 10.0.2.39
- Puerto: 8080
- Base de datos: MySQL en ec2-data (10.0.2.129:3306)

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
3. Despliega en EC2 via AWS SSM

## Variables de entorno
| Variable | Descripción |
|----------|-------------|
| DB_ENDPOINT | IP del servidor MySQL |
| DB_PORT | Puerto MySQL (3306) |
| DB_NAME | Nombre de la base de datos |
| DB_USERNAME | Usuario MySQL |
| DB_PASSWORD | Contraseña MySQL |