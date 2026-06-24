# SURROGATE KEYS

## Definición

Una Surrogate Key es una clave artificial generada por el Data Warehouse para identificar de forma única cada registro de una Dimension Table.

No tiene significado para el negocio.

Su único propósito es:

```text
Identificar registros
de manera única y estable.
```

---

# ¿Por qué existen?

Los sistemas operacionales utilizan:

```text
Business Keys
```

Ejemplo:

```text
CustomerID = CUST100
```

---

Pero los Business Keys pueden:

- Cambiar
- Repetirse entre sistemas
- No ser únicos globalmente
- Tener diferentes formatos

---

Los Data Warehouses necesitan:

```text
Claves estables.
```

---

Por eso utilizan:

```text
Surrogate Keys.
```

---

# Ejemplo

Sistema Fuente:

| CustomerID | CustomerName |
|------------|--------------|
| CUST100 | Pedro |

---

Data Warehouse:

| CustomerKey | CustomerID | CustomerName |
|------------|------------|--------------|
| 10 | CUST100 | Pedro |

---

Observación:

```text
CustomerKey
```

es:

```text
Surrogate Key
```

---

Mientras que:

```text
CustomerID
```

es:

```text
Business Key
```

---

# Características

Una Surrogate Key:

- Es generada por el Data Warehouse.
- No tiene significado para el negocio.
- Nunca cambia.
- Es utilizada para relacionar tablas.

---

# ¿Cómo se generan?

Normalmente mediante:

```text
IDENTITY

SEQUENCE

AUTO_INCREMENT

UUID
```

---

Ejemplo:

| CustomerKey |
|--------------|
| 1 |
| 2 |
| 3 |

---

# Arquitectura

```text
DimCustomer
        ↓

CustomerKey

        ↓

FactSales
```

---

La Fact Table referencia:

```text
Surrogate Keys
```

---

No Business Keys.

---

# Ejemplo Completo

## DimCustomer

| CustomerKey | CustomerID | CustomerName |
|------------|------------|--------------|
| 10 | CUST100 | Pedro |

---

## FactSales

| CustomerKey | SalesAmount |
|------------|-------------|
| 10 | 1500 |

---

Relación:

```text
CustomerKey
```

---

# Relación con SCD Type 2

Antes:

| CustomerKey | CustomerID | City |
|------------|------------|------|
| 10 | CUST100 | Miami |

---

Cambio:

```text
Orlando
```

---

Después:

| CustomerKey | CustomerID | City |
|------------|------------|------|
| 10 | CUST100 | Miami |
| 11 | CUST100 | Orlando |

---

Observación:

El:

```text
Business Key
```

permanece igual.

---

Pero cambia:

```text
Surrogate Key
```

---

Gracias a esto:

```text
Podemos conservar historial.
```

---

# Beneficios

## Estabilidad

No depende del sistema fuente.

---

## Integración

Permite combinar múltiples sistemas.

---

## Historial

Fundamental para SCD Type 2.

---

## Rendimiento

Las claves enteras suelen ser más eficientes para realizar JOINs que cadenas de texto largas.

---

## Independencia

El Data Warehouse controla sus propias claves.

---

# Caso Real

Empresa:

```text
CRM

ERP

E-commerce
```

---

Los tres sistemas utilizan:

```text
CustomerID
```

con formatos diferentes.

---

Data Warehouse:

```text
Genera:

CustomerKey
```

---

Resultado:

```text
Modelo consistente.
```

---

# Surrogate Key vs Business Key

| Característica | Surrogate Key | Business Key |
|---------------|---------------|--------------|
| Generada por | Data Warehouse | Sistema Fuente |
| Significado | No | Sí |
| Cambia | No | Puede cambiar |
| Uso | Relaciones internas | Identificación del negocio |
| Tipo común | Entero | Código de negocio |

---

# Buenas prácticas

## Utilizar enteros

Reducen almacenamiento y mejoran rendimiento.

---

## Nunca reutilizar valores

Cada clave debe ser única.

---

## Mantener el Business Key

Siempre conservar el identificador original para trazabilidad.

---

## Utilizar Surrogate Keys en todas las dimensiones

Especialmente cuando existe historial.

---

## Evitar lógica de negocio

La clave no debe contener información.

---

Ejemplo incorrecto:

```text
CUST-USA-001
```

---

Ejemplo correcto:

```text
101
```

---

# Error común

Muchos principiantes utilizan:

```text
CustomerID
```

como clave primaria del Data Warehouse.

---

Problemas:

- Cambios en el sistema fuente.
- Integración compleja.
- Dificultades con SCD Type 2.

---

# Error conceptual frecuente

Muchos creen:

```text
Surrogate Key
=
Reemplazar Business Key.
```

---

Incorrecto.

Normalmente:

```text
Ambas se almacenan.
```

---

Ejemplo:

| CustomerKey | CustomerID |
|------------|------------|
| 10 | CUST100 |

---

Cada una cumple un propósito diferente.

---

# Caso de Entrevista

Pregunta:

```text
¿Por qué utilizar
Surrogate Keys
en un Data Warehouse?
```

---

Respuesta:

```text
Porque proporcionan identificadores estables,
independientes de los sistemas fuente,
facilitan la integración de datos
y permiten implementar correctamente
Slowly Changing Dimensions,
especialmente SCD Type 2.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar una dimensión pregúntate:

1. ¿Cuál es el Business Key?
2. ¿Necesito historial?
3. ¿Podría cambiar el identificador del sistema fuente?
4. ¿Integraré múltiples sistemas?
5. ¿Qué clave utilizará la Fact Table?
6. ¿La clave será estable a largo plazo?
7. ¿Cómo afectará a las relaciones del modelo?

---

# Relación con los siguientes módulos

```text
SLOWLY CHANGING DIMENSIONS
        ↓
SURROGATE KEYS
        ↓
BUSINESS KEYS
        ↓
DATE DIMENSION
        ↓
JUNK DIMENSIONS
```

---

# Resumen

Las Surrogate Keys son claves artificiales generadas por el Data Warehouse para identificar registros de forma única y estable.

Características principales:

- No tienen significado de negocio.
- Son generadas por el Data Warehouse.
- Permiten integrar múltiples fuentes.
- Mejoran el rendimiento de las relaciones.
- Son fundamentales para implementar SCD Type 2.

En un modelo dimensional moderno, las Fact Tables normalmente se relacionan con las Dimension Tables mediante Surrogate Keys, mientras que los Business Keys se conservan para mantener la trazabilidad con los sistemas de origen.
