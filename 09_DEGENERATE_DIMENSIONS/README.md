# DEGENERATE DIMENSIONS

## Definición

Una Degenerate Dimension es un atributo de negocio almacenado directamente en una Fact Table porque no requiere una Dimension Table propia.

Generalmente corresponde a identificadores transaccionales que no poseen atributos descriptivos adicionales.

---

# ¿Por qué existen?

Supongamos una venta.

La Fact Table almacena:

```text
Cliente

Producto

Fecha

Cantidad

Ventas
```

---

Pero también existe:

```text
Número de Pedido
```

---

Pregunta:

```text
¿Necesitamos crear una
DimOrder?
```

---

Respuesta:

```text
No.
```

---

Si el número de pedido únicamente identifica la transacción y no tiene atributos descriptivos, entonces:

```text
Debe permanecer
en la Fact Table.
```

---

# Concepto Fundamental

Una Degenerate Dimension:

```text
No tiene
Dimension Table.
```

---

Se almacena directamente dentro de:

```text
Fact Table
```

---

# Ejemplo

## FactSales

| OrderNumber | CustomerKey | ProductKey | SalesAmount |
|-------------|------------|------------|-------------|
| ORD-1001 | 10 | 100 | 1500 |

---

Observación:

```text
OrderNumber
```

no posee:

```text
Nombre

Categoría

Ciudad

Marca

Fecha
```

---

Solo identifica:

```text
La transacción.
```

---

# ¿Por qué no crear una Dimensión?

Crear:

```text
DimOrder
```

sería:

| OrderNumber |
|--------------|
| ORD-1001 |

---

No aporta información adicional.

---

Resultado:

```text
Join innecesario.
```

---

# Arquitectura

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

Dentro de FactSales:

```text
OrderNumber
```

permanece directamente.

---

# Características

Una Degenerate Dimension:

- No posee atributos descriptivos.
- No necesita tabla propia.
- Identifica una transacción.
- Vive dentro de la Fact Table.

---

# Ejemplos Comunes

## Número de Pedido

```text
OrderNumber
```

---

## Número de Factura

```text
InvoiceNumber
```

---

## Número de Ticket

```text
TicketNumber
```

---

## Número de Reclamo

```text
ClaimNumber
```

---

## Número de Reserva

```text
ReservationNumber
```

---

Todos son:

```text
Identificadores.
```

---

# Ejemplo Completo

## FactSales

| OrderNumber | DateKey | CustomerKey | ProductKey | SalesAmount |
|-------------|----------|------------|------------|-------------|
| ORD-1001 | 1 | 10 | 100 | 1500 |

---

DimCustomer

| CustomerKey | CustomerName |
|------------|--------------|
| 10 | Pedro |

---

DimProduct

| ProductKey | ProductName |
|------------|-------------|
| 100 | Laptop |

---

Interpretación:

```text
Pedido ORD-1001

Pedro

compró una Laptop

por 1500.
```

---

# Cuándo utilizar Degenerate Dimensions

Cuando el atributo:

- Identifica la transacción.
- No tiene descripción adicional.
- No requiere historial.
- No será reutilizado por otros procesos.

---

# Cuándo NO utilizarla

Si el atributo posee información descriptiva.

---

Ejemplo:

```text
Producto
```

---

Tiene:

```text
Marca

Categoría

Color

Proveedor
```

---

Debe existir:

```text
DimProduct
```

---

No una Degenerate Dimension.

---

# Beneficios

## Menos joins

Consultas más simples.

---

## Modelo más limpio

Evita dimensiones innecesarias.

---

## Mejor rendimiento

Reduce relaciones.

---

## Menor mantenimiento

No existen tablas adicionales.

---

# Caso Real

## Empresa Retail

FactSales

| OrderNumber | CustomerKey | SalesAmount |
|-------------|------------|-------------|

---

Pregunta:

```text
Mostrar el detalle
del pedido ORD-1001.
```

---

Respuesta:

```text
Buscar directamente
por OrderNumber.
```

---

Sin necesidad de:

```text
DimOrder
```

---

# Comparación

## Dimension Table

Contiene:

```text
Atributos descriptivos.
```

---

Ejemplo:

```text
DimCustomer

Nombre

Ciudad

Segmento
```

---

## Degenerate Dimension

Contiene:

```text
Solo un identificador.
```

---

Ejemplo:

```text
OrderNumber
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es una Degenerate Dimension?
```

---

Respuesta:

```text
Es un atributo de negocio,
generalmente un identificador
transaccional,
que se almacena directamente
en la Fact Table porque no
requiere una Dimension Table propia.
```

---

# Buenas prácticas

## Utilizar únicamente identificadores

No almacenar atributos descriptivos.

---

## Evitar crear dimensiones innecesarias

Si no agregan contexto.

---

## Mantener nombres claros

Ejemplo:

```text
OrderNumber

InvoiceNumber

TicketNumber
```

---

## Documentar su propósito

Facilita el mantenimiento.

---

# Error común

Muchos principiantes crean:

```text
DimOrder
```

con una única columna:

```text
OrderNumber
```

---

Resultado:

```text
Join innecesario.

Mayor complejidad.

Sin beneficios.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Toda clave
debe tener
una dimensión.
```

---

Incorrecto.

Si el atributo:

```text
Solo identifica
una transacción
```

puede almacenarse directamente en la Fact Table.

---

# Pensamiento de Data Warehouse

Antes de crear una dimensión pregúntate:

1. ¿Tiene atributos descriptivos?
2. ¿Será reutilizada por otros procesos?
3. ¿Necesita historial?
4. ¿Solo identifica una transacción?
5. ¿Agregar una dimensión aporta valor?
6. ¿Estoy evitando joins innecesarios?
7. ¿El modelo será más simple?

---

# Relación con los siguientes módulos

```text
CONFORMED DIMENSIONS
        ↓
DEGENERATE DIMENSIONS
        ↓
FACTLESS FACT TABLES
        ↓
AGGREGATE FACT TABLES
```

---

# Resumen

Una Degenerate Dimension es un identificador transaccional almacenado directamente en una Fact Table.

Características principales:

- No tiene Dimension Table.
- No posee atributos descriptivos.
- Identifica transacciones.
- Reduce joins innecesarios.

Ejemplos comunes:

- OrderNumber
- InvoiceNumber
- TicketNumber
- ClaimNumber
- ReservationNumber

Es un patrón de diseño ampliamente utilizado en modelos dimensionales basados en la metodología de Ralph Kimball.
