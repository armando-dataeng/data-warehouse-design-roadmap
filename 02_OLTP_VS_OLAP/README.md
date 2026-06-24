# OLTP VS OLAP

## Introducción

Los sistemas de datos empresariales suelen dividirse en dos grandes categorías:

```text
OLTP
Online Transaction Processing
```

y

```text
OLAP
Online Analytical Processing
```

---

Aunque ambos almacenan datos, fueron diseñados para resolver problemas completamente diferentes.

---

# ¿Qué es OLTP?

OLTP significa:

```text
Online Transaction Processing
```

---

Su objetivo es:

```text
Registrar operaciones del negocio.
```

---

Ejemplos:

```text
Crear un pedido

Registrar un pago

Actualizar un cliente

Transferir dinero

Registrar una venta
```

---

# Características de OLTP

## Alta cantidad de transacciones

Miles o millones por día.

---

## Operaciones cortas

Ejemplo:

```sql
INSERT INTO Orders
VALUES (...);
```

---

## Datos actuales

La información más reciente es la más importante.

---

## Alta concurrencia

Muchos usuarios simultáneos.

---

## Modelo normalizado

Reduce redundancia.

---

# Ejemplo OLTP

## Sistema E-commerce

Tablas:

```text
Customers

Orders

OrderDetails

Products
```

---

Operación:

```sql
INSERT INTO Orders
(
    CustomerID,
    OrderDate
)
VALUES
(
    100,
    CURRENT_DATE
);
```

---

Objetivo:

```text
Registrar un pedido.
```

---

# ¿Qué es OLAP?

OLAP significa:

```text
Online Analytical Processing
```

---

Su objetivo es:

```text
Analizar información.
```

---

Ejemplos:

```text
Ventas por mes

Ingresos por región

Productos más vendidos

Clientes más rentables
```

---

# Características de OLAP

## Consultas complejas

Involucran:

- JOIN
- GROUP BY
- SUM
- AVG
- COUNT

---

## Datos históricos

Años de información.

---

## Menos escrituras

Principalmente lectura.

---

## Modelo dimensional

Star Schema.

Snowflake Schema.

---

## Optimizado para análisis

Consultas masivas.

---

# Ejemplo OLAP

Consulta:

```sql
SELECT
    d.Year,
    p.Category,
    SUM(f.SalesAmount) AS TotalSales
FROM FactSales f
JOIN DimDate d
    ON f.DateKey = d.DateKey
JOIN DimProduct p
    ON f.ProductKey = p.ProductKey
GROUP BY
    d.Year,
    p.Category;
```

---

Objetivo:

```text
Analizar ventas históricas.
```

---

# Arquitectura Empresarial

```text
Aplicaciones
        ↓

OLTP Database
        ↓

ETL / ELT
        ↓

Data Warehouse
        ↓

OLAP
```

---

# Caso Real

## Empresa Retail

Sistema operacional:

```text
SQL Server
```

---

Función:

```text
Registrar ventas.
```

---

Data Warehouse:

```text
Snowflake
```

---

Función:

```text
Analizar ventas.
```

---

# Comparación General

| Característica | OLTP | OLAP |
|---------------|------|------|
| Objetivo | Operaciones | Análisis |
| Usuarios | Aplicaciones | Analistas |
| Datos | Actuales | Históricos |
| Consultas | Simples | Complejas |
| Escrituras | Muy frecuentes | Pocas |
| Lecturas | Individuales | Masivas |
| Modelo | Normalizado | Dimensional |
| Rendimiento | Transacciones | Agregaciones |

---

# Diseño de Datos

## OLTP

Normalización.

---

Ejemplo:

```text
Customers

Orders

Products
```

---

Separación para evitar redundancia.

---

## OLAP

Desnormalización controlada.

---

Ejemplo:

```text
FactSales

DimCustomer

DimProduct

DimDate
```

---

Optimización para consultas.

---

# Preguntas OLTP

Ejemplos:

```text
¿Existe este cliente?

¿Cuál es el saldo actual?

¿Qué productos hay disponibles?
```

---

# Preguntas OLAP

Ejemplos:

```text
¿Cuáles fueron las ventas del último año?

¿Qué región genera más ingresos?

¿Qué cliente es más rentable?
```

---

# Rendimiento

## OLTP

Optimizado para:

```text
INSERT

UPDATE

DELETE
```

---

## OLAP

Optimizado para:

```text
SELECT

GROUP BY

Aggregations
```

---

# Ejemplo Visual

## OLTP

```text
Cliente realiza pedido
        ↓

Base de datos registra pedido
```

---

## OLAP

```text
Miles de pedidos
        ↓

Data Warehouse
        ↓

Análisis de ventas
```

---

# Tecnologías Comunes

## OLTP

- SQL Server
- PostgreSQL
- MySQL
- Oracle

---

## OLAP

- Snowflake
- BigQuery
- Redshift
- Synapse

---

# Error común

Muchos principiantes ejecutan:

```sql
SELECT
    SUM(...)
```

sobre bases OLTP gigantes.

---

Resultado:

```text
Bloqueos

Lentitud

Problemas de rendimiento
```

---

# Solución

Mover análisis a:

```text
Data Warehouse
```

---

# Error conceptual frecuente

Muchos creen:

```text
OLTP y OLAP son competidores.
```

---

Incorrecto.

Son complementarios.

---

Arquitectura correcta:

```text
OLTP
      ↓

ETL / ELT
      ↓

OLAP
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia
entre OLTP y OLAP?
```

---

Respuesta:

```text
OLTP está diseñado para registrar
transacciones operacionales.

OLAP está diseñado para analizar
grandes volúmenes de datos históricos.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar una solución pregúntate:

1. ¿Registraré operaciones o analizaré datos?
2. ¿Necesito transacciones rápidas?
3. ¿Necesito análisis históricos?
4. ¿Qué volumen de consultas existe?
5. ¿Qué tipo de usuarios consumirán los datos?
6. ¿Necesito normalización o modelado dimensional?
7. ¿Cuál es el objetivo del sistema?

---

# Relación con los siguientes módulos

```text
DATA WAREHOUSE FUNDAMENTALS
        ↓
OLTP VS OLAP
        ↓
DIMENSIONAL MODELING
        ↓
STAR SCHEMA
```

---

# Resumen

OLTP y OLAP tienen objetivos distintos.

OLTP:

- Operaciones
- Transacciones
- Datos actuales
- Normalización

OLAP:

- Análisis
- Históricos
- Agregaciones
- Modelado dimensional

Las arquitecturas modernas utilizan ambos:

```text
OLTP
      ↓
ETL / ELT
      ↓
OLAP
```

para separar procesamiento operacional y analítico de forma eficiente.
