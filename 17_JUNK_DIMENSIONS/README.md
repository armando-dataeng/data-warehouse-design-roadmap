# JUNK DIMENSIONS

## Definición

Una Junk Dimension es una Dimension Table que agrupa múltiples atributos de baja cardinalidad que no pertenecen naturalmente a una dimensión específica.

Su objetivo es reducir el número de columnas en las Fact Tables y evitar la creación de dimensiones innecesarias.

---

# ¿Por qué existen?

Supongamos una Fact Table de ventas.

Además de las claves principales:

```text
CustomerKey

ProductKey

DateKey
```

también existen atributos como:

```text
Payment Method

Order Priority

Sales Channel

Promotion Applied

Gift Wrapped
```

---

Pregunta:

```text
¿Debemos crear
cinco dimensiones
diferentes?
```

---

Respuesta:

```text
No.
```

---

Todos estos atributos tienen:

```text
Pocos valores posibles.
```

---

La solución es:

```text
Junk Dimension.
```

---

# Concepto Fundamental

Una Junk Dimension agrupa:

```text
Atributos pequeños

+

Baja cardinalidad
```

---

Ejemplos:

```text
Sí / No

Online / Store

Cash / Credit Card

High / Medium / Low
```

---

# Arquitectura

Sin Junk Dimension:

```text
FactSales

PaymentType

Priority

Channel

GiftFlag

PromotionFlag
```

---

Con Junk Dimension:

```text
DimJunk
       ↓

FactSales
```

---

La Fact Table queda más limpia.

---

# Ejemplo

## FactSales

| CustomerKey | ProductKey | JunkKey | SalesAmount |
|--------------|------------|----------|-------------|
| 10 | 100 | 5 | 1500 |

---

## DimJunk

| JunkKey | PaymentType | Channel | Priority | Gift |
|----------|-------------|----------|-----------|------|
| 5 | Credit Card | Online | High | Yes |

---

Interpretación:

```text
La venta fue:

Pago con tarjeta

Canal online

Alta prioridad

Con envoltura de regalo
```

---

# ¿Qué es Baja Cardinalidad?

Cardinalidad:

```text
Cantidad de valores distintos.
```

---

Ejemplo:

## Baja cardinalidad

```text
Yes

No
```

---

```text
Online

Store
```

---

```text
High

Medium

Low
```

---

## Alta cardinalidad

```text
Customer Name

Email

Phone Number

Product Name
```

---

Estos NO pertenecen a una Junk Dimension.

---

# Caso Real

Empresa de E-commerce.

Atributos:

```text
Payment Method

Coupon Used

Gift Wrap

Order Priority

Sales Channel
```

---

Todos tienen pocos valores.

---

Se agrupan en:

```text
DimJunk
```

---

# Beneficios

## Reduce columnas

La Fact Table permanece simple.

---

## Evita dimensiones pequeñas

No crear:

```text
DimPriority

DimGift

DimPayment
```

---

## Mejor organización

Los atributos relacionados permanecen juntos.

---

## Fácil mantenimiento

Una sola dimensión.

---

# Ejemplo Completo

## DimJunk

| JunkKey | Payment | Priority | Gift | Channel |
|----------|----------|-----------|------|----------|
| 1 | Cash | High | No | Store |
| 2 | Card | Medium | Yes | Online |
| 3 | Card | Low | No | Store |

---

## FactSales

| CustomerKey | ProductKey | JunkKey | SalesAmount |
|--------------|------------|----------|-------------|
| 10 | 100 | 2 | 1500 |

---

# ¿Cómo construir una Junk Dimension?

## Paso 1

Identificar atributos pequeños.

---

Ejemplo:

```text
Payment

Priority

Gift

Channel
```

---

## Paso 2

Identificar todas las combinaciones posibles.

---

Ejemplo:

```text
Cash

Card
```

↓

```text
Online

Store
```

↓

```text
High

Medium

Low
```

---

## Paso 3

Asignar una Surrogate Key.

---

Ejemplo:

| JunkKey | Payment | Channel |
|----------|----------|----------|
| 1 | Cash | Store |
| 2 | Card | Online |

---

# Cuándo utilizar Junk Dimensions

Cuando existen:

```text
Muchos atributos

↓

Con pocos valores posibles.
```

---

# Cuándo NO utilizarlas

Si los atributos tienen:

```text
Alta cardinalidad.
```

---

Ejemplo:

```text
CustomerName

Email

ProductName
```

---

Esos pertenecen a dimensiones independientes.

---

# Buenas prácticas

## Agrupar atributos relacionados

Mantener coherencia.

---

## Evitar atributos de alta cardinalidad

No pertenecen a una Junk Dimension.

---

## Mantener pocas columnas

Solo las necesarias.

---

## Documentar las combinaciones

Facilita mantenimiento.

---

## Utilizar una Surrogate Key

Como cualquier dimensión.

---

# Error común

Muchos principiantes crean:

```text
DimPayment

DimPriority

DimGift

DimChannel
```

---

Resultado:

```text
Demasiadas dimensiones pequeñas.

Mayor cantidad de joins.

Modelo innecesariamente complejo.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Junk Dimension

=

Guardar datos basura.
```

---

Incorrecto.

El nombre:

```text
Junk
```

se refiere a:

```text
Pequeños atributos

que no encajan

naturalmente

en otra dimensión.
```

---

No significa:

```text
Información sin valor.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es una Junk Dimension?
```

---

Respuesta:

```text
Es una Dimension Table que agrupa múltiples atributos de baja cardinalidad para reducir el número de columnas en las Fact Tables y evitar la creación de dimensiones innecesarias.
```

---

# Pensamiento de Data Warehouse

Antes de crear una Junk Dimension pregúntate:

1. ¿Los atributos tienen baja cardinalidad?
2. ¿Realmente necesitan una dimensión propia?
3. ¿Pueden agruparse lógicamente?
4. ¿Estoy simplificando la Fact Table?
5. ¿La combinación de valores será manejable?
6. ¿Qué impacto tendrá en las consultas?
7. ¿Será fácil mantener esta dimensión?

---

# Relación con los siguientes módulos

```text
ROLE-PLAYING DIMENSIONS
        ↓
JUNK DIMENSIONS
        ↓
BRIDGE TABLES
        ↓
DATA MARTS
        ↓
KIMBALL METHODOLOGY
```

---

# Resumen

Las Junk Dimensions permiten agrupar atributos de baja cardinalidad en una única dimensión.

Características principales:

- Reducen columnas en las Fact Tables.
- Evitan crear múltiples dimensiones pequeñas.
- Mejoran la organización del modelo.
- Utilizan una Surrogate Key como cualquier dimensión.

Ejemplos comunes:

- Método de pago
- Canal de venta
- Prioridad
- Uso de cupón
- Envoltura de regalo

Son un patrón de diseño recomendado por Ralph Kimball para mantener modelos dimensionales simples, consistentes y fáciles de mantener.
