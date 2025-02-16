# Configuración de PostgreSQL con Docker

## **Requisitos previos**

- Tener [Docker](https://www.docker.com/products/docker-desktop/) instalado.
- Conocimientos básicos de PostgreSQL y Docker.

## **Paso 1: Verificar Docker**

Para asegurarte de que Docker está instalado, ejecuta en la terminal:

```bash
docker --version
```
![image](https://github.com/user-attachments/assets/944e72fe-78a9-4abf-aa61-b77a1f9f043a)

Si muestra la versión de Docker, significa que está instalado correctamente.

---

## **Paso 2: Descargar la imagen de PostgreSQL**

Ejecuta el siguiente comando para descargar la imagen oficial de PostgreSQL:

```bash
docker pull postgres
```
![image](https://github.com/user-attachments/assets/6bd9d701-8a87-409f-8915-abc7aad0e978)

---

## **Paso 3: Crear y ejecutar un contenedor con PostgreSQL**

Ejecuta el siguiente comando para crear y ejecutar el contenedor:

```bash
docker run --name mi_postgres -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=admin123 -e POSTGRES_DB=mi_base -p 5432:5432 -d postgres
```
![image](https://github.com/user-attachments/assets/39e7f009-03e3-44ee-b3a5-0822892c341a)

📌 **Parámetros:**
- `--name mi_postgres` → Nombre del contenedor.
- `-e POSTGRES_USER=admin` → Usuario de la base de datos.
- `-e POSTGRES_PASSWORD=admin123` → Contraseña.
- `-e POSTGRES_DB=mi_base` → Nombre de la base de datos.
- `-p 5432:5432` → Expone el puerto 5432.
- `-d postgres` → Ejecuta en segundo plano.

Verifica que el contenedor está corriendo con:

```bash
docker ps
```
![image](https://github.com/user-attachments/assets/992e1f80-bcd2-4538-abc1-225624c93527)

---

## **Paso 4: Conectarse a PostgreSQL dentro del contenedor**

Ejecuta el siguiente comando para ingresar al contenedor y conectarte a PostgreSQL:

```bash
docker exec -it mi_postgres psql -U admin -d mi_base
```
![image](https://github.com/user-attachments/assets/1533436d-0cd2-4d5b-afd1-7c4e61152dea)

---

## **Paso 5: Crear la tabla "Estudiante"**

Dentro de la consola de PostgreSQL, ejecuta:

```sql
CREATE TABLE Estudiante (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    edad INT,
    correo VARCHAR(100) UNIQUE,
    fecha_registro TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
![image](https://github.com/user-attachments/assets/6d664b08-1554-4c8c-bf99-4dc42f1ef942)

Verifica que la tabla fue creada con:

```sql
\d Estudiante
```
![image](https://github.com/user-attachments/assets/30c74319-389e-42f5-a93a-5496deaa9f82)

---

## **Paso 6: Insertar y consultar datos**

Para insertar un estudiante:

```sql
INSERT INTO Estudiante (nombre, edad, correo) VALUES ('Juan Pérez', 22, 'juanperez@gmail.com');
```
![image](https://github.com/user-attachments/assets/3fe77424-4d0c-4be7-886b-179bfb2d95e6)

Consulta los datos:

```sql
SELECT * FROM Estudiante;
```
![image](https://github.com/user-attachments/assets/493cff39-d820-4871-9ce8-7003763ccb36)

---

## **Paso 7: Salir y detener el contenedor**

Para salir de PostgreSQL:

```sql
\q
```
![image](https://github.com/user-attachments/assets/4000c6c0-bece-489f-a7ce-080dfd57e690)

Para detener el contenedor:

```bash
docker stop mi_postgres
```
![image](https://github.com/user-attachments/assets/5d253a56-24d7-4702-9a41-dd9251143d76)

Para iniciarlo nuevamente:

```bash
docker start mi_postgres
```
![image](https://github.com/user-attachments/assets/f159fc0c-9ca2-450f-9be1-6e5e82afc494)

Con estos pasos, ya tienes PostgreSQL corriendo en Docker con una base de datos y una tabla funcional.
