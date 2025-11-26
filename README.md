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

---

## 📝 4. Paso 1: Creación del Esquema (Schema SQL)

En el panel *Schema SQL* pega lo siguiente:

```sql
-- Crear tabla de Licenciaturas
CREATE TABLE licenciaturas (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
);

-- Crear tabla de Alumnos
CREATE TABLE alumnos (
  id SERIAL PRIMARY KEY,
  nombre VARCHAR(100),
  apellido VARCHAR(100),
  semestre INT,
  id_licenciatura INT,
  FOREIGN KEY (id_licenciatura) REFERENCES licenciaturas(id)
);
```

---

## 💾 5. Paso 2: Inserción de Datos

```sql
-- Insertar licenciaturas de FMAT (UADY)
INSERT INTO licenciaturas (nombre) VALUES
('Matemáticas'),
('Actuaría'),
('Ingeniería de Software'),
('Ciencia de Datos'),
('Computación Aplicada');

-- Insertar alumnos
INSERT INTO alumnos (nombre, apellido, semestre, id_licenciatura) VALUES
('Adrián', 'Cab', 2, 1),        -- Matemáticas
('Gabriel', 'Cuadros', 4, 3),   -- Ingeniería de Software
('Lucy', 'Fernández', 1, 2),    -- Actuaría
('Diego', 'Pérez', 6, 4),       -- Ciencia de Datos
('Santiago', 'Valdez', 3, 5);   -- Computación Aplicada
```

> Haz clic en **"Ejecutar"** para crear la base y cargar datos.

---

## 🔍 6. Paso 3: Ejecutar Consultas (Query SQL)

### **Consulta A: Ver todas las licenciaturas**

```sql
SELECT * FROM licenciaturas;
```

### **Consulta B: Ver todos los alumnos**

```sql
SELECT * FROM alumnos;
```

### **Consulta C: Reporte completo (JOIN alumnos–licenciaturas)**

```sql
SELECT a.nombre, a.apellido, a.semestre, l.nombre AS licenciatura
FROM alumnos a
JOIN licenciaturas l ON a.id_licenciatura = l.id;
```

### **Consulta D (opcional): Alumnos por licenciatura específica**

```sql
SELECT a.nombre, a.apellido, a.semestre
FROM alumnos a
JOIN licenciaturas l ON a.id_licenciatura = l.id
WHERE l.nombre = 'Matemáticas';
```

---

## ✅ 8. Evidencia a entregar

En el Forms deberás subir:

* Una captura de pantalla de DB-Fiddle mostrando el resultado de la **Consulta C**.

---
