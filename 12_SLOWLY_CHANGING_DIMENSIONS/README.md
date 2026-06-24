# SLOWLY CHANGING DIMENSIONS (SCD)

## Definición

Las Slowly Changing Dimensions (SCD) son técnicas utilizadas para administrar los cambios en los atributos de una Dimension Table a lo largo del tiempo.

Su objetivo es responder una pregunta fundamental:

```text
¿Qué hacemos cuando
cambia un dato
de una dimensión?
```

---

# ¿Por qué existen?

Supongamos la siguiente dimensión:

## DimCustomer

| CustomerKey | CustomerName | City |
|------------|--------------|------|
| 10 | Pedro | Miami |

---

Un año después:

Pedro se muda a:

```text
Orlando
```

---

Pregunta:

```text
¿Actualizamos el registro?

¿Creamos uno nuevo?

¿Guardamos ambos?
```

---

La respuesta depende del tipo de SCD.

---

# ¿Qué es una Slowly Changing Dimension?

Una dimensión cuyos atributos cambian con poca frecuencia.

---

Ejemplos:

```text
Ciudad

Estado Civil

Dirección

Departamento

Cargo

Segmento
```

---

No cambian constantemente, pero sí con el tiempo.

---

# Tipos de SCD

Los más utilizados son:

```text
Type 0

Type 1

Type 2

Type 3
```

---

# SCD Type 0

## Definición

Nunca permite cambios.

---

Los datos permanecen iguales para siempre.

---

Ejemplo:

```text
Fecha de nacimiento
```

---

Antes:

| Customer | BirthDate |
|----------|-----------|
| Pedro | 1995-05-10 |

---

Después:

```text
Sin cambios.
```

---

Uso:

```text
Datos permanentes.
```

---

# SCD Type 1

## Definición

Sobrescribe el valor anterior.

No conserva historial.

---

Ejemplo

Antes:

| Customer | City |
|----------|------|
| Pedro | Miami |

---

Cambio:

```text
Orlando
```

---

Después:

| Customer | City |
|----------|------|
| Pedro | Orlando |

---

Resultado:

```text
Miami desaparece.
```

---

Ventajas

- Muy simple.
- Poco almacenamiento.

---

Desventajas

```text
Se pierde historial.
```

---

# SCD Type 2

## Definición

Conserva historial creando un nuevo registro.

Es el tipo más utilizado en Data Warehousing.

---

Antes:

| CustomerKey | Customer | City |
|-------------|----------|------|
| 10 | Pedro | Miami |

---

Cambio:

```text
Orlando
```

---

Después:

| CustomerKey | Customer | City | Current |
|-------------|----------|------|----------|
| 10 | Pedro | Miami | No |
| 11 | Pedro | Orlando | Yes |

---

Ahora existen:

```text
Dos versiones.
```

---

Normalmente se agregan columnas como:

```text
StartDate

EndDate

IsCurrent
```

---

Ejemplo:

| CustomerKey | City | StartDate | EndDate | IsCurrent |
|-------------|------|-----------|----------|-----------|
| 10 | Miami | 2020 | 2024 | No |
| 11 | Orlando | 2024 | NULL | Yes |

---

Ventajas

- Conserva historial.
- Ideal para análisis históricos.

---

Desventajas

- Mayor almacenamiento.
- Mayor complejidad.

---

# SCD Type 3

## Definición

Conserva únicamente el valor anterior.

---

Ejemplo

| Customer | PreviousCity | CurrentCity |
|----------|--------------|-------------|
| Pedro | Miami | Orlando |

---

Solo guarda:

```text
Valor actual

Valor anterior
```

---

No conserva todo el historial.

---

# Comparación

| Tipo | Conserva Historial | Método |
|------|--------------------|--------|
| Type 0 | Sí | No permite cambios |
| Type 1 | No | Sobrescribe |
| Type 2 | Sí | Nuevo registro |
| Type 3 | Parcial | Columna adicional |

---

# Caso Real

## Cliente cambia de ciudad

Pregunta:

```text
¿Dónde vivía el cliente
cuando realizó una compra
en 2022?
```

---

Type 1:

```text
No podemos saberlo.
```

---

Type 2:

```text
Sí podemos saberlo.
```

---

Por eso:

```text
Type 2
```

es el más utilizado.

---

# Arquitectura Type 2

```text
FactSales
        ↓

CustomerKey

        ↓

DimCustomer
```

---

Cada venta apunta a:

```text
La versión correcta
del cliente.
```

---

# ¿Cuándo utilizar cada tipo?

## Type 0

```text
Información permanente.
```

---

Ejemplos:

- Fecha de nacimiento
- Número de identificación

---

## Type 1

```text
No interesa el historial.
```

---

Ejemplos:

- Corrección ortográfica
- Error de captura

---

## Type 2

```text
Necesitamos historial.
```

---

Ejemplos:

- Dirección
- Ciudad
- Departamento
- Segmento

---

## Type 3

```text
Solo interesa el cambio anterior.
```

---

Ejemplos:

- Cambio de gerente
- Cambio de categoría

---

# Buenas prácticas

## Definir qué atributos requieren historial

No todos lo necesitan.

---

## Utilizar Surrogate Keys

Especialmente con Type 2.

---

## Agregar fechas de vigencia

Facilitan análisis históricos.

---

## Marcar registro actual

Ejemplo:

```text
IsCurrent = Yes
```

---

## Documentar el tipo SCD utilizado

Facilita mantenimiento.

---

# Error común

Muchos principiantes utilizan:

```text
Type 1
```

para todas las dimensiones.

---

Resultado:

```text
Pérdida de historial.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Type 2
```

es siempre la mejor opción.

---

Incorrecto.

Depende del negocio.

Conservar historial implica:

- Mayor almacenamiento.
- Mayor complejidad.
- Mayor mantenimiento.

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia entre
SCD Type 1 y Type 2?
```

---

Respuesta:

```text
Type 1 sobrescribe los datos
y pierde el historial.

Type 2 crea un nuevo registro
para conservar todas las versiones
históricas de la dimensión.
```

---

# Pensamiento de Data Warehouse

Antes de elegir un tipo SCD pregúntate:

1. ¿Necesito conservar historial?
2. ¿Qué impacto tiene perderlo?
3. ¿Qué atributos cambian con el tiempo?
4. ¿Qué volumen de cambios espero?
5. ¿Cómo afectará a las Fact Tables?
6. ¿Qué consultas realizará el negocio?
7. ¿Cuál es el costo de mantener versiones históricas?

---

# Relación con los siguientes módulos

```text
AGGREGATE FACT TABLES
        ↓
SLOWLY CHANGING DIMENSIONS
        ↓
SURROGATE KEYS
        ↓
BUSINESS KEYS
        ↓
DATE DIMENSION
```

---

# Resumen

Las Slowly Changing Dimensions permiten administrar cambios en las dimensiones de un Data Warehouse.

Tipos principales:

- Type 0 → Sin cambios.
- Type 1 → Sobrescribe.
- Type 2 → Conserva historial.
- Type 3 → Conserva el valor anterior.

En la práctica, **SCD Type 2** es el patrón más utilizado porque permite realizar análisis históricos sin perder información sobre cómo evolucionaron los datos del negocio.
