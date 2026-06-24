# ROLE-PLAYING DIMENSIONS

## Definición

Una Role-Playing Dimension es una misma Dimension Table que desempeña diferentes roles dentro de una Fact Table.

En lugar de crear múltiples dimensiones con la misma información, se reutiliza una sola dimensión mediante diferentes claves foráneas.

---

# ¿Por qué existen?

Supongamos una empresa de logística.

Cada pedido tiene:

```text
Fecha del Pedido

Fecha de Envío

Fecha de Entrega
```

---

Pregunta:

```text
¿Necesitamos crear
tres tablas DimDate?
```

---

Respuesta:

```text
No.
```

---

Todas representan:

```text
Fechas.
```

---

Por lo tanto:

```text
Se reutiliza
la misma DimDate.
```

---

# Concepto Fundamental

Una misma dimensión puede representar distintos conceptos dependiendo del contexto.

Ejemplo:

```text
DimDate
```

puede actuar como:

```text
Order Date

Ship Date

Delivery Date
```

---

# Arquitectura

```text
              DimDate
                 ▲
        ┌────────┼────────┐
        │        │        │
 OrderDate  ShipDate  DeliveryDate
        │        │        │
        └────────┼────────┘
                 │
            FactOrders
```

---

Existe:

```text
Una sola dimensión.
```

---

Pero desempeña:

```text
Tres roles.
```

---

# Ejemplo

## FactOrders

| OrderDateKey | ShipDateKey | DeliveryDateKey | SalesAmount |
|--------------|-------------|-----------------|-------------|
| 20240101 | 20240103 | 20240106 | 1500 |

---

## DimDate

| DateKey | Date | Month | Year |
|----------|------|--------|------|
| 20240101 | 2024-01-01 | January | 2024 |
| 20240103 | 2024-01-03 | January | 2024 |
| 20240106 | 2024-01-06 | January | 2024 |

---

Observación:

```text
DimDate

↓

Se utiliza tres veces.
```

---

# Ejemplo SQL

```sql
SELECT
    od.Month AS OrderMonth,
    sd.Month AS ShipMonth,
    dd.Month AS DeliveryMonth,
    SUM(f.SalesAmount) AS TotalSales
FROM FactOrders f
JOIN DimDate od
    ON f.OrderDateKey = od.DateKey
JOIN DimDate sd
    ON f.ShipDateKey = sd.DateKey
JOIN DimDate dd
    ON f.DeliveryDateKey = dd.DateKey
GROUP BY
    od.Month,
    sd.Month,
    dd.Month;
```

---

Cada alias representa:

```text
Un rol diferente.
```

---

# Otro Ejemplo

Empresa de Recursos Humanos.

Empleado:

```text
Fecha de Contratación

Fecha de Promoción

Fecha de Retiro
```

---

Todas utilizan:

```text
DimDate
```

---

# Más Ejemplos

## FactFlights

```text
DepartureDate

ArrivalDate
```

↓

```text
DimDate
```

---

## FactPayments

```text
InvoiceDate

DueDate

PaymentDate
```

↓

```text
DimDate
```

---

## FactProjects

```text
StartDate

EndDate

ReviewDate
```

↓

```text
DimDate
```

---

# Beneficios

## Reutilización

Una sola dimensión.

---

## Consistencia

Mismos atributos temporales.

---

## Menor mantenimiento

No existen dimensiones duplicadas.

---

## Menor almacenamiento

Una única DimDate.

---

# Diferencia con Conformed Dimensions

## Conformed Dimension

Compartida entre:

```text
Varias Fact Tables.
```

---

Ejemplo:

```text
FactSales

FactReturns

FactInventory
```

↓

```text
DimProduct
```

---

## Role-Playing Dimension

Compartida:

```text
Dentro de la misma Fact Table.
```

---

Ejemplo:

```text
OrderDate

ShipDate

DeliveryDate
```

↓

```text
DimDate
```

---

# Caso Real

Empresa de E-commerce.

FactOrders

| OrderDateKey | ShipDateKey | DeliveryDateKey |
|--------------|-------------|-----------------|

---

Pregunta:

```text
¿Cuál es el tiempo promedio
entre pedido y entrega?
```

---

Respuesta:

```text
Utilizando la misma
DimDate
```

para ambos eventos.

---

# Buenas prácticas

## Utilizar alias claros

Ejemplo:

```text
OrderDate

ShipDate

DeliveryDate
```

---

## Reutilizar la dimensión

Evitar duplicar tablas.

---

## Documentar cada rol

Facilitar mantenimiento.

---

## Mantener una única fuente

Todos los roles deben utilizar la misma dimensión.

---

## Pensar en el negocio

Cada clave debe representar un evento distinto.

---

# Error común

Muchos principiantes crean:

```text
DimOrderDate

DimShipDate

DimDeliveryDate
```

---

Resultado:

```text
Duplicación

Mayor mantenimiento

Mayor almacenamiento
```

---

# Error conceptual frecuente

Muchos creen:

```text
Cada fecha
requiere una dimensión.
```

---

Incorrecto.

Normalmente:

```text
Una sola DimDate

↓

Múltiples roles.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es una
Role-Playing Dimension?
```

---

Respuesta:

```text
Es una dimensión que se reutiliza múltiples veces dentro de una Fact Table para representar distintos roles del mismo tipo de información.

El ejemplo más común es una DimDate utilizada como fecha de pedido, envío y entrega.
```

---

# Pensamiento de Data Warehouse

Antes de crear una nueva dimensión pregúntate:

1. ¿Representa realmente una entidad diferente?
2. ¿Puedo reutilizar una dimensión existente?
3. ¿Solo cambia el contexto?
4. ¿Necesito diferentes atributos?
5. ¿Estoy duplicando información?
6. ¿Qué tan fácil será mantener el modelo?
7. ¿Los usuarios entenderán cada rol?

---

# Relación con los siguientes módulos

```text
DATE DIMENSION
        ↓
ROLE-PLAYING DIMENSIONS
        ↓
JUNK DIMENSIONS
        ↓
BRIDGE TABLES
        ↓
DATA MARTS
```

---

# Resumen

Las Role-Playing Dimensions permiten reutilizar una misma Dimension Table para representar distintos roles dentro de una Fact Table.

Características principales:

- Una sola dimensión.
- Múltiples claves foráneas.
- Menor redundancia.
- Mayor consistencia.
- Modelo más fácil de mantener.

El caso más común es una **DimDate** utilizada simultáneamente como:

- Order Date
- Ship Date
- Delivery Date

Este patrón es ampliamente utilizado en Data Warehouses modernos y forma parte de las mejores prácticas del modelado dimensional propuesto por Ralph Kimball.
