# DIMENSION TABLES

## Definición

Una Dimension Table almacena atributos descriptivos que proporcionan contexto a los eventos registrados en una Fact Table.

Permiten responder preguntas como:

```text
¿Quién compró?

¿Qué producto se vendió?

¿Cuándo ocurrió?

¿Dónde ocurrió?
```

---

# ¿Por qué existen?

Supongamos la siguiente Fact Table:

| CustomerKey | ProductKey | SalesAmount |
|------------|------------|-------------|
| 10 | 100 | 1500 |

---

Pregunta:

```text
¿Quién es el cliente 10?

¿Qué producto es el 100?
```

---

La Fact Table no responde estas preguntas.

---

Las respuestas viven en:

```text
Dimension Tables
```

---

# Concepto Fundamental

Las dimensiones proporcionan:

```text
Contexto
```

a las métricas almacenadas en las Fact Tables.

---

# Arquitectura General

```text
DimCustomer
        ↓

     FactSales

        ↑

DimProduct

        ↑

DimDate
```

---

# Ejemplo Básico

## FactSales

| CustomerKey | ProductKey | SalesAmount |
|------------|------------|-------------|
| 10 | 100 | 1500 |

---

## DimCustomer

| CustomerKey | CustomerName |
|------------|--------------|
| 10 | Pedro |

---

## DimProduct

| ProductKey | ProductName |
|------------|-------------|
| 100 | Laptop |

---

Interpretación:

```text
Pedro compró una Laptop
por 1500.
```

---

# Características

Las Dimension Tables suelen:

```text
Ser más pequeñas

Contener atributos descriptivos

Cambiar lentamente

Tener muchas columnas
```

---

Las Fact Tables suelen:

```text
Ser más grandes

Contener métricas

Crecer rápidamente
```

---

# Componentes de una Dimensión

## Surrogate Key

Clave técnica utilizada en el Data Warehouse.

---

Ejemplo:

```text
CustomerKey = 10
```

---

## Business Key

Clave proveniente del sistema fuente.

---

Ejemplo:

```text
CustomerID = CUST100
```

---

## Attributes

Información descriptiva.

---

Ejemplo:

```text
Nombre

Ciudad

País

Segmento

Estado
```

---

# Ejemplo Completo

## DimCustomer

| CustomerKey | CustomerID | CustomerName | City | Country |
|------------|------------|--------------|------|---------|
| 10 | CUST100 | Pedro | Miami | USA |

---

# Tipos de Dimensiones

## Customer Dimension

Información de clientes.

---

Ejemplo:

```text
Nombre

Ciudad

Segmento

País
```

---

# Product Dimension

Información de productos.

---

Ejemplo:

```text
Producto

Marca

Categoría

Proveedor
```

---

# Date Dimension

Información temporal.

---

Ejemplo:

| DateKey | Date | Month | Quarter | Year |
|----------|------|--------|---------|------|

---

Muy utilizada en análisis.

---

# Geography Dimension

Información geográfica.

---

Ejemplo:

```text
Ciudad

Estado

País

Región
```

---

# Employee Dimension

Información organizacional.

---

Ejemplo:

```text
Empleado

Departamento

Cargo
```

---

# Jerarquías

Concepto muy importante.

---

Ejemplo:

```text
Ciudad
    ↓

Estado
    ↓

País
```

---

Permite análisis por niveles.

---

Ejemplo:

```text
Ventas por Ciudad

Ventas por Estado

Ventas por País
```

---

# Dimensión de Fecha

La dimensión más utilizada.

---

## Ejemplo

| DateKey | Day | Month | Quarter | Year |
|----------|-----|--------|---------|------|

---

Beneficios:

```text
Evita cálculos repetitivos.

Facilita análisis temporal.
```

---

# Atributos Descriptivos

Una dimensión puede contener:

```text
Nombre

Categoría

Marca

Color

Tamaño

Segmento
```

---

Su objetivo:

```text
Describir entidades del negocio.
```

---

# Diseño de Dimensiones

## Correcto

```text
DimProduct

Producto
Marca
Categoría
Color
```

---

## Incorrecto

Guardar estas columnas en:

```text
FactSales
```

---

Eso genera:

```text
Duplicación

Mayor almacenamiento

Problemas de mantenimiento
```

---

# Caso Real

## Retail

Fact Table:

```text
FactSales
```

---

Dimensiones:

```text
DimCustomer

DimProduct

DimStore

DimDate
```

---

Pregunta:

```text
Ventas por categoría
y país.
```

---

Las dimensiones permiten responderla fácilmente.

---

# Star Schema

Las dimensiones suelen ser:

```text
Desnormalizadas.
```

---

Ejemplo:

## DimCustomer

| CustomerKey | Name | City | Country |
|------------|------|------|---------|

---

Beneficio:

```text
Menos joins.
```

---

# Snowflake Schema

Las dimensiones pueden normalizarse.

---

Ejemplo:

```text
DimCustomer
      ↓

DimCity
      ↓

DimCountry
```

---

Beneficio:

```text
Menor redundancia.
```

---

# Buenas prácticas

## Utilizar Surrogate Keys

Evitar dependencias de sistemas fuente.

---

## Mantener atributos descriptivos

No almacenar métricas.

---

## Diseñar jerarquías claramente

Facilitar análisis.

---

## Utilizar nombres comprensibles

Pensar en usuarios de negocio.

---

## Documentar atributos

Facilitar mantenimiento.

---

# Error común

Muchos principiantes almacenan:

```text
SalesAmount

Quantity

Profit
```

en una dimensión.

---

Incorrecto.

Esas son:

```text
Métricas
```

y pertenecen a:

```text
Fact Tables
```

---

# Error conceptual frecuente

Muchos creen:

```text
Dimension Table
=
Tabla pequeña.
```

---

Incorrecto.

Algunas dimensiones pueden contener:

```text
Millones de registros.
```

---

Lo importante es:

```text
Su función descriptiva.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es una Dimension Table?
```

---

Respuesta:

```text
Es una tabla que almacena atributos descriptivos utilizados para proporcionar contexto a las métricas almacenadas en una Fact Table.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Cuál es la diferencia entre
una Fact Table y una Dimension Table?
```

---

Respuesta:

```text
Las Fact Tables almacenan eventos y métricas.

Las Dimension Tables almacenan contexto y atributos descriptivos que permiten analizar esas métricas.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar una dimensión pregúntate:

1. ¿Qué entidad representa?
2. ¿Qué atributos necesita el negocio?
3. ¿Existen jerarquías?
4. ¿Necesito historial?
5. ¿Qué consultas realizarán los usuarios?
6. ¿Utilizaré Surrogate Keys?
7. ¿Cómo evolucionará la dimensión en el tiempo?

---

# Relación con los siguientes módulos

```text
FACT TABLES
        ↓
DIMENSION TABLES
        ↓
CONFORMED DIMENSIONS
        ↓
DEGENERATE DIMENSIONS
        ↓
SCD TYPES
```

---

# Resumen

Las Dimension Tables proporcionan contexto a las métricas almacenadas en las Fact Tables.

Conceptos principales:

- Surrogate Keys
- Business Keys
- Attributes
- Hierarchies
- Date Dimension

Su objetivo es facilitar el análisis y permitir que los usuarios entiendan el significado de los datos almacenados en el Data Warehouse.
