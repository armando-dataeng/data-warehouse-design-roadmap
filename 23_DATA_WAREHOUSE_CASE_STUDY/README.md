# DATA WAREHOUSE CASE STUDY

## Objetivo

En este caso de estudio construiremos un Data Warehouse para una empresa de Retail aplicando todos los conceptos aprendidos a lo largo del repositorio.

Al finalizar seremos capaces de diseñar una arquitectura analítica completa, desde los sistemas fuente hasta los Data Marts.

---

# Escenario

La empresa:

```text
TechStore
```

vende productos tecnológicos a través de:

```text
Tiendas físicas

E-commerce

Marketplace
```

---

La dirección necesita responder preguntas como:

```text
¿Cuáles son los productos más vendidos?

¿Cuál es la rentabilidad por categoría?

¿Qué clientes generan más ingresos?

¿Cuáles son las ventas por región?

¿Cómo evolucionan las ventas mes a mes?
```

---

Actualmente la información se encuentra distribuida en varios sistemas.

---

# Sistemas Fuente

## CRM

Información de clientes.

---

Ejemplo:

```text
Customers

Addresses

Contacts
```

---

## ERP

Información financiera.

---

Ejemplo:

```text
Orders

Invoices

Payments
```

---

## E-commerce

Información de ventas online.

---

Ejemplo:

```text
Orders

Products

Coupons
```

---

## Inventario

Información de stock.

---

Ejemplo:

```text
Warehouses

Inventory

Suppliers
```

---

# Arquitectura

```text
CRM

ERP

E-commerce

Inventory

        ↓

ETL / ELT

        ↓

Enterprise Data Warehouse

        ↓

Sales Data Mart

        ↓

Power BI
```

---

# Paso 1

## Identificar procesos del negocio

Procesos principales:

```text
Ventas

Inventario

Clientes

Pagos
```

---

Para este caso trabajaremos con:

```text
Ventas.
```

---

# Paso 2

## Definir el Grain

Pregunta:

```text
¿Qué representa
una fila?
```

---

Respuesta:

```text
Una línea de venta
por producto.
```

---

Ejemplo:

Pedido:

```text
1001
```

Productos:

```text
Laptop

Mouse
```

---

Resultado:

```text
Dos filas
en FactSales.
```

---

# Paso 3

## Identificar dimensiones

Se utilizarán:

```text
DimCustomer

DimProduct

DimDate

DimStore

DimSalesperson
```

---

# Paso 4

## Diseñar Fact Table

FactSales

| DateKey | ProductKey | CustomerKey | StoreKey | Quantity | SalesAmount |
|----------|------------|-------------|----------|----------|-------------|

---

Medidas:

```text
Quantity

SalesAmount

CostAmount

ProfitAmount
```

---

# Paso 5

## Diseñar DimCustomer

| CustomerKey | CustomerID | CustomerName | City | Country |
|-------------|------------|--------------|------|---------|

---

Utilizar:

```text
Surrogate Key
```

---

Conservar:

```text
Business Key
```

---

# Paso 6

## Diseñar DimProduct

| ProductKey | ProductName | Brand | Category |
|------------|-------------|-------|----------|

---

# Paso 7

## Diseñar DimDate

| DateKey | Date | Month | Quarter | Year |
|----------|------|--------|----------|------|

---

# Paso 8

## Crear Star Schema

```text
                 DimDate
                    |
                    |

DimCustomer -- FactSales -- DimProduct
                    |
                    |

              DimStore
```

---

# Paso 9

## Implementar SCD Type 2

Caso:

Cliente cambia de ciudad.

Antes:

```text
Miami
```

---

Después:

```text
Orlando
```

---

DimCustomer

| CustomerKey | CustomerID | City | IsCurrent |
|-------------|------------|------|-----------|
| 10 | CUST100 | Miami | No |
| 11 | CUST100 | Orlando | Yes |

---

Ahora el historial permanece disponible.

---

# Paso 10

## Crear Data Mart

Sales Mart

Contiene:

```text
FactSales

DimCustomer

DimProduct

DimDate

DimStore
```

---

Optimizado para:

```text
Dashboards
```

---

# Consultas Analíticas

## Ventas por Categoría

```sql
SELECT
    p.Category,
    SUM(f.SalesAmount) AS TotalSales
FROM FactSales f
JOIN DimProduct p
    ON f.ProductKey = p.ProductKey
GROUP BY p.Category;
```

---

## Ventas por Mes

```sql
SELECT
    d.Month,
    SUM(f.SalesAmount) AS TotalSales
FROM FactSales f
JOIN DimDate d
    ON f.DateKey = d.DateKey
GROUP BY d.Month;
```

---

## Top 10 Clientes

```sql
SELECT
    c.CustomerName,
    SUM(f.SalesAmount) AS Revenue
FROM FactSales f
JOIN DimCustomer c
    ON f.CustomerKey = c.CustomerKey
GROUP BY c.CustomerName
ORDER BY Revenue DESC
LIMIT 10;
```

---

# KPIs

El Data Warehouse permitirá construir indicadores como:

```text
Ventas Totales

Cantidad Vendida

Ticket Promedio

Margen de Ganancia

Clientes Activos

Ventas por Región

Ventas por Categoría

Ventas por Canal
```

---

# Herramientas BI

El Sales Mart puede ser consumido por:

```text
Power BI

Tableau

Looker
```

---

# Flujo Completo

```text
Operational Systems

↓

ETL / ELT

↓

Enterprise Data Warehouse

↓

Sales Data Mart

↓

Dashboards

↓

Decisiones de negocio
```

---

# Conceptos Aplicados

Durante este caso de estudio utilizamos:

- OLTP vs OLAP
- Enterprise Data Warehouse
- Star Schema
- Fact Tables
- Dimension Tables
- Grain
- Conformed Dimensions
- Surrogate Keys
- Business Keys
- Date Dimension
- Slowly Changing Dimensions (Type 2)
- Data Marts
- Kimball Methodology

---

# Buenas prácticas

## Definir correctamente el Grain

Es la decisión más importante del modelo.

---

## Mantener dimensiones compartidas

Facilitan la integración.

---

## Utilizar Surrogate Keys

Permiten gestionar historial.

---

## Conservar Business Keys

Facilitan ETL y auditoría.

---

## Diseñar para el negocio

Pensar primero en las preguntas que deberán responder los usuarios.

---

# Resultado Final

Arquitectura completa:

```text
CRM
ERP
E-commerce
Inventory

        ↓

ETL / ELT

        ↓

Enterprise Data Warehouse

        ↓

Sales Data Mart

        ↓

Power BI
```

---

# Lecciones Aprendidas

Al finalizar este caso de estudio serás capaz de:

- Identificar procesos de negocio.
- Definir el grain de una Fact Table.
- Diseñar dimensiones y métricas.
- Construir un Star Schema.
- Implementar SCD Type 2.
- Utilizar Surrogate y Business Keys.
- Diseñar un Data Mart.
- Aplicar la metodología Kimball.
- Comprender la relación entre un Enterprise Data Warehouse y los Data Marts.
- Construir una solución analítica lista para herramientas de Business Intelligence.

---

# Resumen

En este caso de estudio construimos un Data Warehouse para una empresa de Retail siguiendo un enfoque profesional de modelado dimensional.

Se aplicaron conceptos como:

- Star Schema
- Fact Tables
- Dimension Tables
- Data Marts
- Enterprise Data Warehouse
- Slowly Changing Dimensions
- Surrogate Keys
- Kimball Methodology

El resultado es una arquitectura analítica escalable, consistente y preparada para responder preguntas de negocio mediante herramientas de Business Intelligence.
