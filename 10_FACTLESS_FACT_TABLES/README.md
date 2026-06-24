# FACTLESS FACT TABLES

## Definición

Una Factless Fact Table es una Fact Table que no almacena medidas numéricas.

Su propósito es registrar la ocurrencia de un evento o la relación entre dimensiones.

En otras palabras:

```text
Registra que algo ocurrió,
pero no cuánto ocurrió.
```

---

# ¿Por qué existen?

La mayoría de las Fact Tables almacenan métricas.

Ejemplo:

```text
Ventas

Cantidad

Costo

Ganancia
```

---

Pero existen procesos donde solo importa saber:

```text
Que el evento ocurrió.
```

---

Ejemplos:

```text
Un estudiante asistió a clase.

Un cliente visitó una tienda.

Un empleado asistió a un curso.

Un paciente acudió a una consulta.
```

---

No existe una medida.

Solo:

```text
La ocurrencia del evento.
```

---

# Concepto Fundamental

Una Factless Fact Table contiene:

```text
Foreign Keys

+

Ninguna medida
```

---

Ejemplo:

## FactAttendance

| StudentKey | CourseKey | DateKey |
|------------|-----------|----------|
| 100 | 20 | 1 |

---

Interpretación:

```text
El estudiante 100

asistió

al curso 20

en la fecha 1.
```

---

# Arquitectura

```text
DimStudent
       ↓

FactAttendance

       ↑

DimCourse

       ↑

DimDate
```

---

No existen métricas.

---

# ¿Qué almacena?

Solo relaciones entre dimensiones.

---

Ejemplo:

```text
Cliente

Producto

Fecha
```

---

Indican:

```text
Que ocurrió un evento.
```

---

# Tipos de Factless Fact Tables

## Event Tracking

Registran eventos.

---

Ejemplos:

```text
Asistencia

Visitas

Reservas

Inscripciones
```

---

## Coverage Tables

Registran situaciones esperadas.

---

Ejemplo:

```text
Productos disponibles
por tienda.
```

---

Permiten responder:

```text
¿Qué productos
NO fueron vendidos?
```

---

# Ejemplo 1

## Asistencia Escolar

FactAttendance

| StudentKey | CourseKey | DateKey |
|------------|-----------|----------|
| 10 | 100 | 1 |

---

Consulta:

```text
¿Cuántos estudiantes
asistieron?
```

---

SQL:

```sql
SELECT COUNT(*)
FROM FactAttendance;
```

---

No existe una columna:

```text
AttendanceCount
```

---

Cada fila representa:

```text
Una asistencia.
```

---

# Ejemplo 2

## Visitas a Tiendas

FactStoreVisit

| CustomerKey | StoreKey | DateKey |
|------------|----------|----------|
| 50 | 2 | 1 |

---

Interpretación:

```text
El cliente visitó la tienda.
```

---

No existe:

```text
Monto

Cantidad

Ventas
```

---

# Ejemplo 3

## Registro de Cursos

FactEnrollment

| StudentKey | CourseKey | SemesterKey |
|------------|-----------|-------------|
| 20 | 5 | 20241 |

---

Permite responder:

```text
¿Cuántos estudiantes
se inscribieron?
```

---

# Event Fact vs Factless Fact

## Fact Table

Contiene:

```text
SalesAmount

Quantity

Profit
```

---

## Factless Fact Table

Contiene:

```text
Solo claves.
```

---

# Beneficios

## Registrar eventos

---

## Reducir complejidad

---

## Facilitar conteos

---

## Representar relaciones

---

# Caso Real

## Hospital

FactAppointment

| PatientKey | DoctorKey | DateKey |
|------------|-----------|----------|

---

Pregunta:

```text
¿Cuántas consultas
realizó cada médico?
```

---

Consulta:

```sql
SELECT
    DoctorKey,
    COUNT(*)
FROM FactAppointment
GROUP BY DoctorKey;
```

---

Cada fila representa:

```text
Una consulta médica.
```

---

# Coverage Fact Table

Caso interesante.

---

Supongamos:

```text
Todos los productos
que deberían estar
en cada tienda.
```

---

FactCoverage

| ProductKey | StoreKey |
|------------|----------|

---

Luego comparar con:

```text
FactSales
```

---

Permite responder:

```text
¿Qué productos
no se vendieron?
```

---

# Comparación

| Característica | Fact Table | Factless Fact Table |
|---------------|------------|---------------------|
| Medidas | Sí | No |
| Foreign Keys | Sí | Sí |
| Eventos | Sí | Sí |
| Conteos | Sí | Sí |
| Métricas | Sí | No |

---

# Cuándo utilizar Factless Fact Tables

Cuando:

```text
Solo interesa saber
que ocurrió un evento.
```

---

O cuando:

```text
Necesitamos registrar
una relación entre dimensiones.
```

---

# Buenas prácticas

## Definir claramente el evento

Cada fila debe representar un único evento.

---

## Mantener un grain consistente

Ejemplo:

```text
Una fila por asistencia.
```

---

## Utilizar únicamente Foreign Keys

Evitar atributos descriptivos.

---

## No agregar medidas innecesarias

Si existe una métrica real, probablemente ya no sea una Factless Fact Table.

---

# Error común

Muchos principiantes agregan:

```text
AttendanceCount = 1
```

---

No es necesario.

---

Cada fila ya representa:

```text
Una asistencia.
```

---

Puede utilizarse:

```sql
COUNT(*)
```

---

# Error conceptual frecuente

Muchos creen:

```text
Fact Table
=
Siempre contiene métricas.
```

---

Incorrecto.

Las Factless Fact Tables almacenan:

```text
Eventos

Relaciones
```

---

Sin medidas numéricas.

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es una Factless Fact Table?
```

---

Respuesta:

```text
Es una Fact Table que no almacena medidas numéricas.

Su objetivo es registrar eventos o relaciones entre dimensiones, permitiendo realizar análisis mediante conteos y asociaciones.
```

---

# Pensamiento de Data Warehouse

Antes de crear una Factless Fact Table pregúntate:

1. ¿Existe realmente una medida?
2. ¿Solo necesito registrar que ocurrió un evento?
3. ¿Cuál será el grain?
4. ¿Qué dimensiones participan?
5. ¿Las consultas serán principalmente conteos?
6. ¿Estoy evitando columnas innecesarias?
7. ¿El modelo representa correctamente el proceso de negocio?

---

# Relación con los siguientes módulos

```text
DEGENERATE DIMENSIONS
        ↓
FACTLESS FACT TABLES
        ↓
AGGREGATE FACT TABLES
        ↓
SLOWLY CHANGING DIMENSIONS
```

---

# Resumen

Las Factless Fact Tables permiten modelar procesos donde no existen medidas numéricas.

Características principales:

- No almacenan métricas.
- Contienen únicamente Foreign Keys.
- Registran eventos o relaciones.
- Se utilizan principalmente para conteos y análisis de ocurrencias.

Casos comunes:

- Asistencia
- Visitas
- Inscripciones
- Reservas
- Cobertura de productos

Son un patrón avanzado del modelado dimensional ampliamente utilizado en Data Warehouses empresariales y forman parte de la metodología de Ralph Kimball.
