# FACT TABLES

## Definición

Una Fact Table es la tabla central de un modelo dimensional que almacena eventos del negocio y sus métricas asociadas.

Representa:

```text
Qué ocurrió.
```

---

# ¿Por qué existe?

Las empresas necesitan medir:

```text
Ventas

Ingresos

Costos

Pagos

Transacciones

Inventario
```

---

Estas mediciones se almacenan en:

```text
Fact Tables
```

---

# Concepto Fundamental

Una Fact Table almacena:

```text
Métricas
+
Claves de dimensiones
```

---

Ejemplo:

## FactSales

| DateKey | ProductKey | CustomerKey | SalesAmount |
|----------|------------|------------|-------------|
| 1 | 100 | 10 | 1500 |

---

Interpretación:

```text
Cliente 10

compró

Producto 100

en Fecha 1

por 1500
```

---

# Componentes de una Fact Table

## Foreign Keys

Referencias a dimensiones.

---

Ejemplo:

```text
DateKey

CustomerKey

ProductKey

StoreKey
```

---

## Measures

Métricas del negocio.

---

Ejemplos:

```text
Quantity

SalesAmount

CostAmount

ProfitAmount
```

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

La Fact Table conecta dimensiones.

---

# Grain (Granularidad)

Concepto más importante.

---

## Definición

El grain define:

```text
¿Qué representa una fila?
```

---

Antes de diseñar una Fact Table siempre debemos responder esta pregunta.

---

# Ejemplo

Grain:

```text
Una fila por producto vendido.
```

---

Datos:

| OrderID | ProductID | Quantity |
|----------|-----------|----------|
| 100 | A | 2 |
| 100 | B | 1 |

---

Resultado:

```text
2 filas
```

---

Porque:

```text
Cada fila representa
un producto vendido.
```

---

# Grain Incorrecto

Error común:

```text
No definir el grain.
```

---

Resultado:

```text
Duplicados

Consultas incorrectas

Métricas inconsistentes
```

---

# Ejemplo de Grain

## Nivel Pedido

```text
Una fila por pedido.
```

---

## Nivel Línea de Pedido

```text
Una fila por producto vendido.
```

---

## Nivel Diario

```text
Una fila por día.
```

---

Cada decisión produce un modelo diferente.

---

# Fact Table Ejemplo

## FactSales

| DateKey | CustomerKey | ProductKey | Quantity | SalesAmount |
|----------|------------|------------|----------|-------------|
| 1 | 10 | 100 | 2 | 1500 |

---

Foreign Keys:

```text
DateKey

CustomerKey

ProductKey
```

---

Measures:

```text
Quantity

SalesAmount
```

---

# Tipos de Fact Tables

## Transaction Fact Table

La más común.

---

Representa:

```text
Eventos individuales.
```

---

Ejemplos:

```text
Ventas

Pagos

Pedidos
```

---

Grain:

```text
Una fila por transacción.
```

---

# Snapshot Fact Table

Captura estado en un momento específico.

---

Ejemplo:

```text
Inventario diario.
```

---

Datos:

| DateKey | ProductKey | Inventory |
|----------|------------|-----------|
| 1 | 100 | 500 |

---

# Accumulating Snapshot

Representa procesos con etapas.

---

Ejemplo:

```text
Pedido
↓
Empaque
↓
Envío
↓
Entrega
```

---

Fact Table:

| OrderKey | OrderDate | ShipDate | DeliveryDate |
|-----------|-----------|-----------|-------------|

---

Permite medir:

```text
Tiempo de entrega
```

---

# Medidas Aditivas

## Definición

Se pueden sumar en todas las dimensiones.

---

Ejemplos:

```text
SalesAmount

Quantity

Revenue
```

---

Consulta:

```sql
SUM(SalesAmount)
```

---

# Medidas Semi-Aditivas

Se pueden sumar parcialmente.

---

Ejemplo:

```text
Account Balance
```

---

Se puede sumar:

```text
Por cliente
```

---

Pero no:

```text
Por tiempo
```

---

# Medidas No Aditivas

No deben sumarse.

---

Ejemplos:

```text
Porcentajes

Promedios

Ratios
```

---

# Fact Table de Ventas

## Diseño

```text
FactSales
```

---

Claves:

```text
DateKey

CustomerKey

ProductKey

StoreKey
```

---

Métricas:

```text
Quantity

SalesAmount

CostAmount

ProfitAmount
```

---

# Caso Real

## Retail

Pregunta:

```text
¿Cuáles fueron las ventas
por categoría y mes?
```

---

Consulta:

```sql
SELECT
    d.Month,
    p.Category,
    SUM(f.SalesAmount)
FROM FactSales f
JOIN DimDate d
    ON f.DateKey = d.DateKey
JOIN DimProduct p
    ON f.ProductKey = p.ProductKey
GROUP BY
    d.Month,
    p.Category;
```

---

# Buenas prácticas

## Definir el grain primero

Siempre.

---

## Utilizar Surrogate Keys

Evitar claves de negocio en la Fact Table.

---

## Mantener solo métricas

No almacenar atributos descriptivos.

---

## Diseñar para consultas

Pensar en cómo se consumirá la información.

---

## Evitar cálculos complejos

Calcular métricas derivadas en capas analíticas cuando sea posible.

---

# Error común

Muchos principiantes agregan:

```text
CustomerName

ProductName

City
```

directamente en la Fact Table.

---

Incorrecto.

Esos atributos pertenecen a:

```text
Dimension Tables
```

---

# Error conceptual frecuente

Muchos creen:

```text
Fact Table
=
Tabla más grande
```

---

Incorrecto.

Una Fact Table es:

```text
La tabla que almacena
eventos y métricas del negocio.
```

---

Puede ser grande o pequeña.

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es una Fact Table?
```

---

Respuesta:

```text
Es la tabla central de un modelo dimensional que almacena eventos del negocio, métricas y referencias a dimensiones para soportar análisis y reporting.
```

---

# Pregunta de Entrevista Avanzada

Pregunta:

```text
¿Cuál es el concepto más importante
al diseñar una Fact Table?
```

---

Respuesta:

```text
Definir correctamente el grain,
ya que determina qué representa cada fila y afecta todas las métricas y consultas futuras.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar una Fact Table pregúntate:

1. ¿Cuál es el proceso de negocio?
2. ¿Qué representa una fila?
3. ¿Qué métricas necesito analizar?
4. ¿Qué dimensiones darán contexto?
5. ¿Las métricas son aditivas?
6. ¿Cuál será el volumen de datos?
7. ¿Qué consultas ejecutarán los usuarios?

---

# Relación con los siguientes módulos

```text
STAR SCHEMA
        ↓
FACT TABLES
        ↓
DIMENSION TABLES
        ↓
CONFORMED DIMENSIONS
```

---

# Resumen

Las Fact Tables son el núcleo del modelado dimensional.

Conceptos principales:

- Grain
- Measures
- Foreign Keys
- Transaction Facts
- Snapshot Facts
- Accumulating Snapshots

Su función es almacenar eventos y métricas del negocio para soportar análisis, reporting y Business Intelligence de forma eficiente.
