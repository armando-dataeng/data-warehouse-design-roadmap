# DIMENSIONAL MODELING

## Definición

Dimensional Modeling es una técnica de diseño utilizada en Data Warehouses para organizar datos de forma que las consultas analíticas sean simples, rápidas y fáciles de entender.

Fue popularizada por:

```text
Ralph Kimball
```

y es la base de la mayoría de las soluciones de Business Intelligence modernas.

---

# ¿Por qué existe?

Los modelos OLTP están optimizados para:

```text
INSERT

UPDATE

DELETE
```

---

Pero los analistas necesitan responder preguntas como:

```text
¿Cuánto vendimos el último año?

¿Cuál es el producto más vendido?

¿Qué región genera más ingresos?

¿Qué clientes son más rentables?
```

---

Las bases normalizadas no son ideales para este tipo de consultas.

---

Por eso surge:

```text
Dimensional Modeling
```

---

# Objetivo

Organizar los datos para facilitar:

- Consultas analíticas
- Reportes
- Dashboards
- Agregaciones
- Business Intelligence

---

# Concepto Principal

Todo modelo dimensional se construye alrededor de:

```text
Facts
+
Dimensions
```

---

# Facts

Representan:

```text
Eventos del negocio.
```

---

Ejemplos:

```text
Ventas

Pedidos

Pagos

Transacciones

Llamadas
```

---

Normalmente contienen:

```text
Métricas
```

---

Ejemplos:

```text
Cantidad

Ventas

Costo

Ganancia
```

---

# Dimensions

Representan:

```text
Contexto del negocio.
```

---

Ejemplos:

```text
Cliente

Producto

Fecha

Sucursal

Región
```

---

Las dimensiones responden:

```text
Quién

Qué

Cuándo

Dónde
```

---

# Ejemplo Simple

## Pregunta

```text
¿Cuánto vendimos por producto?
```

---

Fact Table:

```text
FactSales
```

---

Dimension:

```text
DimProduct
```

---

Consulta:

```text
Ventas
agrupadas
por Producto
```

---

# Arquitectura General

```text
Dimensions
        ↓

      Fact

        ↑

Dimensions
```

---

Ejemplo:

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

# Fact Table

Contiene:

```text
Métricas
```

---

Ejemplo:

## FactSales

| DateKey | ProductKey | CustomerKey | SalesAmount |
|----------|-----------|-------------|-------------|
| 1 | 100 | 10 | 1500 |

---

# Dimension Tables

Contienen:

```text
Descripciones.
```

---

## DimProduct

| ProductKey | ProductName |
|------------|--------------|
| 100 | Laptop |

---

## DimCustomer

| CustomerKey | CustomerName |
|------------|--------------|
| 10 | Pedro |

---

## DimDate

| DateKey | Month |
|---------|-------|
| 1 | January |

---

# Interpretación

```text
Pedro compró una Laptop
en Enero
por 1500.
```

---

# Ventajas

## Consultas Simples

Menos joins.

---

## Mejor rendimiento

Optimizado para análisis.

---

## Fácil comprensión

Modelo cercano al negocio.

---

## Escalabilidad

Funciona bien con grandes volúmenes.

---

# Granularidad (Grain)

Concepto fundamental.

---

## Definición

Nivel más bajo de detalle almacenado.

---

Ejemplo:

```text
Una fila por venta.
```

---

O:

```text
Una fila por pedido.
```

---

O:

```text
Una fila por producto vendido.
```

---

# Importancia del Grain

Antes de crear una Fact Table debemos responder:

```text
¿Qué representa una fila?
```

---

Esta es una de las decisiones más importantes del diseño.

---

# Tipos de Hechos

## Additive Facts

Se pueden sumar.

---

Ejemplo:

```text
SalesAmount

Quantity
```

---

# Semi-Additive Facts

Se pueden sumar parcialmente.

---

Ejemplo:

```text
Account Balance
```

---

# Non-Additive Facts

No se deben sumar.

---

Ejemplo:

```text
Porcentajes

Promedios
```

---

# Tipos de Dimensiones

## Customer Dimension

Información de clientes.

---

## Product Dimension

Información de productos.

---

## Date Dimension

Información temporal.

---

## Geography Dimension

Información geográfica.

---

# Star Schema

Modelo más utilizado.

---

Arquitectura:

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

Características:

```text
Simple

Rápido

Popular
```

---

# Snowflake Schema

Versión más normalizada.

---

Ejemplo:

```text
DimProduct
      ↓

DimCategory
      ↓

FactSales
```

---

Características:

```text
Menor redundancia

Más joins
```

---

# Caso Real

## Empresa Retail

Pregunta:

```text
Ventas por categoría
y mes.
```

---

Modelo:

```text
FactSales

DimProduct

DimDate
```

---

Consulta:

```text
SUM(SalesAmount)
GROUP BY
Category,
Month
```

---

# Kimball Methodology

Principios fundamentales:

1. Identificar proceso de negocio.
2. Definir granularidad.
3. Identificar dimensiones.
4. Identificar hechos.

---

Ejemplo:

```text
Proceso:
Ventas
```

---

Grain:

```text
Una fila por producto vendido.
```

---

Dimensiones:

```text
Cliente
Producto
Fecha
```

---

Hechos:

```text
Ventas
Cantidad
Costo
```

---

# Beneficios

## Reporting rápido

---

## Dashboards eficientes

---

## Fácil mantenimiento

---

## Modelo intuitivo

---

## Escalabilidad analítica

---

# Error común

Muchos principiantes diseñan Data Warehouses usando:

```text
Normalización OLTP.
```

---

Resultado:

```text
Consultas complejas.

Muchos joins.

Bajo rendimiento.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Fact Table
=
Tabla más grande.
```

---

Incorrecto.

Una Fact Table es:

```text
La tabla que almacena
medidas del negocio.
```

---

No necesariamente la más grande.

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es Dimensional Modeling?
```

---

Respuesta:

```text
Es una técnica de diseño para Data Warehouses
que organiza datos mediante Fact Tables y
Dimension Tables para facilitar consultas
analíticas y Business Intelligence.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar un modelo dimensional pregúntate:

1. ¿Cuál es el proceso de negocio?
2. ¿Cuál será la granularidad?
3. ¿Qué métricas analizaré?
4. ¿Qué dimensiones darán contexto?
5. ¿Necesito historial?
6. ¿Qué consultas ejecutarán los usuarios?
7. ¿Cómo optimizaré el rendimiento?

---

# Relación con los siguientes módulos

```text
OLTP VS OLAP
        ↓
DIMENSIONAL MODELING
        ↓
STAR SCHEMA
        ↓
SNOWFLAKE SCHEMA
        ↓
FACT TABLES
        ↓
DIMENSION TABLES
```

---

# Resumen

Dimensional Modeling es la técnica de diseño más utilizada en Data Warehouses.

Conceptos fundamentales:

- Facts
- Dimensions
- Grain
- Star Schema
- Snowflake Schema

Su objetivo es construir modelos simples, rápidos y orientados al análisis para soportar Business Intelligence y toma de decisiones.
