# STAR SCHEMA

## Definición

Star Schema es un modelo dimensional utilizado en Data Warehouses donde una tabla de hechos (Fact Table) se encuentra en el centro y está rodeada por múltiples tablas de dimensiones (Dimension Tables).

Su nombre proviene de su forma visual:

```text
        Dimension
            |
            |
Dimension -- Fact -- Dimension
            |
            |
        Dimension
```

---

# ¿Por qué existe?

Los analistas necesitan responder preguntas como:

```text
¿Cuánto vendimos?

¿Quién compró?

¿Qué producto se vendió?

¿Cuándo ocurrió?

¿Dónde ocurrió?
```

---

Star Schema organiza los datos para responder estas preguntas de forma rápida y sencilla.

---

# Componentes Principales

Todo Star Schema está compuesto por:

```text
Fact Table
+
Dimension Tables
```

---

# Fact Table

Representa:

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
```

---

Contiene:

```text
Métricas
+
Claves de dimensiones
```

---

# Dimension Tables

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

# Ejemplo Básico

## FactSales

| DateKey | ProductKey | CustomerKey | SalesAmount |
|----------|------------|------------|-------------|
| 1 | 100 | 10 | 1500 |

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

## DimDate

| DateKey | Month |
|---------|--------|
| 1 | January |

---

# Interpretación

```text
Pedro compró una Laptop
en Enero
por 1500.
```

---

# Estructura Visual

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

Por eso recibe el nombre:

```text
Star Schema
```

---

# Diseño Paso a Paso

## Paso 1

Identificar proceso de negocio.

---

Ejemplo:

```text
Ventas
```

---

## Paso 2

Definir granularidad.

---

Pregunta:

```text
¿Qué representa una fila?
```

---

Ejemplo:

```text
Una fila por producto vendido.
```

---

## Paso 3

Identificar dimensiones.

---

Ejemplos:

```text
Cliente

Producto

Fecha

Sucursal
```

---

## Paso 4

Identificar métricas.

---

Ejemplos:

```text
Cantidad

Ventas

Costo

Ganancia
```

---

# Ejemplo Completo

## FactSales

| DateKey | ProductKey | CustomerKey | Quantity | SalesAmount |
|----------|------------|------------|----------|-------------|
| 1 | 100 | 10 | 2 | 1500 |

---

## DimCustomer

| CustomerKey | CustomerName | City |
|------------|--------------|------|
| 10 | Pedro | Miami |

---

## DimProduct

| ProductKey | ProductName | Category |
|------------|-------------|----------|
| 100 | Laptop | Electronics |

---

## DimDate

| DateKey | Year | Month |
|---------|------|-------|
| 1 | 2024 | January |

---

# Consulta Analítica

Pregunta:

```text
Ventas por categoría.
```

---

SQL:

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

# Ventajas

## Simplicidad

Modelo fácil de entender.

---

## Menos Joins

Consultas más sencillas.

---

## Mejor rendimiento

Optimizado para análisis.

---

## Compatible con BI

Ideal para:

- Power BI
- Tableau
- Looker

---

## Escalable

Funciona bien con grandes volúmenes.

---

# Claves en Star Schema

## Surrogate Key

Clave técnica.

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

Normalmente:

```text
Fact Table
```

usa:

```text
Surrogate Keys
```

---

# Tipos de Fact Tables

## Transaction Fact Table

Una fila por transacción.

---

Ejemplo:

```text
Ventas
```

---

## Snapshot Fact Table

Estado en un momento específico.

---

Ejemplo:

```text
Inventario diario.
```

---

## Accumulating Snapshot

Proceso con múltiples etapas.

---

Ejemplo:

```text
Pedido
↓
Envío
↓
Entrega
```

---

# Caso Real

## Retail

Pregunta:

```text
Ventas por ciudad
y mes.
```

---

Modelo:

```text
FactSales

DimCustomer

DimDate
```

---

Consulta:

```text
SUM(SalesAmount)
GROUP BY
City,
Month
```

---

# Star Schema vs OLTP

## OLTP

```text
Normalizado
```

---

Ejemplo:

```text
Customers

Addresses

Cities

Countries
```

---

## Star Schema

```text
Desnormalizado
```

---

Ejemplo:

```text
DimCustomer
```

contiene:

```text
Cliente

Ciudad

País
```

---

Beneficio:

```text
Menos joins.
```

---

# Star Schema vs Snowflake Schema

## Star Schema

```text
Desnormalizado
```

---

Ejemplo:

```text
DimProduct
```

contiene:

```text
Producto
Categoría
Marca
```

---

## Snowflake Schema

```text
Normalizado parcialmente
```

---

Ejemplo:

```text
DimProduct
      ↓

DimCategory
      ↓

DimBrand
```

---

# Cuándo utilizar Star Schema

Ideal cuando:

```text
La simplicidad es prioridad.

Las consultas son analíticas.

El rendimiento es importante.
```

---

# Beneficios para BI

Permite construir fácilmente:

```text
Dashboards

KPIs

Reportes

Análisis históricos
```

---

# Error común

Muchos principiantes diseñan:

```text
Data Warehouse
```

como:

```text
OLTP
```

---

Resultado:

```text
Consultas complejas.

Bajo rendimiento.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Star Schema
=
Modelo sin normalización.
```

---

Incorrecto.

Existe:

```text
Desnormalización controlada.
```

---

Para optimizar análisis.

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es un Star Schema?
```

---

Respuesta:

```text
Es un modelo dimensional donde una Fact Table central se conecta a múltiples Dimension Tables para facilitar consultas analíticas y mejorar el rendimiento del Data Warehouse.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar un Star Schema pregúntate:

1. ¿Cuál es el proceso de negocio?
2. ¿Cuál es el grain?
3. ¿Qué métricas analizaré?
4. ¿Qué dimensiones necesito?
5. ¿Qué consultas ejecutarán los usuarios?
6. ¿Qué volumen manejaré?
7. ¿Cómo optimizaré el rendimiento?

---

# Relación con los siguientes módulos

```text
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

Star Schema es el modelo dimensional más utilizado en Data Warehousing.

Componentes principales:

- Fact Tables
- Dimension Tables

Beneficios:

- Simplicidad
- Rendimiento
- Escalabilidad
- Facilidad de análisis

Es la base de la mayoría de las soluciones modernas de Business Intelligence y Analytics.
