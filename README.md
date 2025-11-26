# Sesion_Practica
Sesión Práctica: Base de Datos

---

# Práctica de Base de Datos: Gestión de Alumnos y Carreras en DB-Fiddle

Actividad práctica para el diseño, implementación y consulta de bases de datos relacionales orientadas a la administración escolar.

---

## 🎯 Aprendizaje esperado

Al finalizar esta actividad, el estudiante será capaz de:

* Comprender cómo estructurar una base de datos para gestionar alumnos y sus carreras.
* Diferenciar entre DDL y DML.
* Crear tablas relacionadas mediante claves foráneas.
* Insertar información realista y consultar datos con SQL (`SELECT`, `WHERE`, `JOIN`).
* Utilizar **DB-Fiddle** como herramienta para prototipado de bases de datos.
* Documentar y compartir resultados mediante enlaces y capturas de pantalla.

---

## 📘 1. Conceptos fundamentales

### ✅ ¿Qué es SQL?

SQL es el lenguaje estándar para administrar bases de datos relacionales: permite crear tablas, insertar datos y consultarlos.

### ✅ DDL vs DML

* **DDL (Data Definition Language)**: crea estructuras.
  Ejemplo: `CREATE TABLE`
* **DML (Data Manipulation Language)**: manipula datos.
  Ejemplo: `INSERT`, `UPDATE`, `SELECT`

---

## 🏫 2. Contexto de la actividad

Crearemos una base de datos para gestionar alumnos de una escuela y las *licenciaturas* pertenecientes a una facultad (ejemplo: **FMAT – UADY**).

Registraremos:

### **Tabla de Licenciaturas**

* Nombre de la licenciatura
  (Ej. Matemáticas, Actuaría, Computación, etc.)

### **Tabla de Alumnos**

* Nombre
* Apellido
* Semestre
* Licenciatura (como llave foránea)

**Nombres a utilizar:**
Adrián Cab
Gabriel Cuadros
Lucy Fernández
Diego Pérez
Santiago Valdez

---

## 🛠️ 3. Configurar el entorno (DB-Fiddle)

Ingresa a:
[https://www.db-fiddle.com/](https://www.db-fiddle.com/)

Motor recomendado:

> **PostgreSQL v15** (o la versión más reciente disponible)

### Identificar los paneles de trabajo

**Panel izquierdo:** Schema SQL
Aquí se colocan las tablas y los datos iniciales.

**Panel derecho:** Query SQL
Aquí se escriben las consultas para obtener información.
---

## 📝 4. Paso 1: Creación del Esquema (Schema SQL)

En el panel *Schema SQL* pega lo siguiente:

```sql
-- TABLA 1: LICENCIATURAS (CARRERAS)
-- Permanece igual.
CREATE TABLE Licenciaturas (
    licenciatura_id INT PRIMARY KEY,
    nombre_licenciatura VARCHAR(150) NOT NULL,
    facultad VARCHAR(100)
);

-- TABLA 2: ALUMNOS (MODIFICADA: SIN MATRÍCULA)
-- Usamos 'alumno_id' como clave primaria.
CREATE TABLE Alumnos (
    alumno_id INT PRIMARY KEY, -- Nuevo campo de identificación
    nombre VARCHAR(50) NOT NULL,
    apellido VARCHAR(50) NOT NULL,
    semestre INT NOT NULL,
    licenciatura_id INT,
    FOREIGN KEY (licenciatura_id) REFERENCES Licenciaturas(licenciatura_id)
);
```
📌 Este paso crea la estructura base de la BD.
> Haz clic en "Ejecutar" para que DB-Fiddle cree las tablas.

---

## 💾 5. Paso 2: Inserción de Datos

Coloca este código debajo del anterior (en el mismo panel Schema SQL):

```sql
-- INSERCIÓN DE DATOS en Licenciaturas (FMAT - UADY)
INSERT INTO Licenciaturas (licenciatura_id, nombre_licenciatura, facultad) VALUES
(100, 'Ingeniería de Software', 'FMAT - UADY'),
(200, 'Licenciatura en Matemáticas', 'FMAT - UADY'),
(300, 'Licenciatura en Actuaría', 'FMAT - UADY'),
(400, 'Licenciatura en Ciencia de Datos', 'FMAT - UADY');

-- INSERCIÓN DE DATOS en Alumnos con los nombres solicitados
INSERT INTO Alumnos (alumno_id, nombre, apellido, semestre, licenciatura_id) VALUES
(1, 'Adrián', 'Cab', 5, 100),       -- Ingeniería de Software
(2, 'Gabriel', 'Cuadros', 3, 200),  -- Licenciatura en Matemáticas
(3, 'Lucy', 'Fernández', 7, 100),   -- Ingeniería de Software
(4, 'Diego', 'Pérez', 1, 300),      -- Licenciatura en Actuaría
(5, 'Santiago', 'Valdez', 5, 400);   -- Licenciatura en Ciencia de Datos
```
📌 Este paso llena la base con datos reales para hacer pruebas.
> Haz clic en **"Ejecutar"** para crear la base y cargar datos.

---

## 🔍 6. Paso 3: Ejecutar Consultas (Query SQL)
Ahora ve al panel Query SQL (lado derecho) y prueba las siguientes consultas.

### **Consulta geeral**

```sql
-- CONSULTA: Obtener el nombre completo, semestre y la licenciatura de cada alumno.
SELECT
    A.nombre,
    A.apellido,
    A.semestre,
    L.nombre_licenciatura AS licenciatura
FROM
    Alumnos A
JOIN
    Licenciaturas L ON A.licenciatura_id = L.licenciatura_id
ORDER BY
    A.apellido;
```

---

## 8. Agregar datos
## Cómo agregar datos nuevos a la tabla

Para agregar datos nuevos solo debes seguir estos pasos:

- Situarte en el ***Schema SQL***.
- Escribir un comando `INSERT INTO ... VALUES(...)` con los valores de los nuevos registros (alumnos, licenciaturas, etc.).
- Ejecutar el comando para insertar los datos en la tabla.

### Ejemplo: agregar un alumno nuevo

```sql
INSERT INTO Alumnos (alumno_id, nombre, apellido, semestre, licenciatura_id) 
VALUES (6, 'Nombre', 'Apellido', 1, 100);
```

> Ingresa tu Nombre y Apellido en el sitio correspondiente 


---

## ✅ 9. Evidencia a entregar

En el Forms deberás subir:

* Una captura de pantalla de DB-Fiddle mostrando el resultado de la **Consulta general** con tus datos, después de haber agregado un alumno nuevo.

---
