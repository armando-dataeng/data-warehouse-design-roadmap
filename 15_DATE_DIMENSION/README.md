# DATE DIMENSION

## Definición

La Date Dimension (DimDate) es una Dimension Table especializada que almacena información relacionada con el calendario.

Su objetivo es proporcionar atributos temporales para facilitar el análisis de datos a lo largo del tiempo.

Es una de las dimensiones más utilizadas en un Data Warehouse.

---

# ¿Por qué existe?

Supongamos la siguiente Fact Table:

| Date | SalesAmount |
|------|-------------|
| 2024-01-15 | 1500 |

---

Pregunta:

```text
¿A qué trimestre pertenece?

¿Fue fin de semana?

¿En qué semana del año ocurrió?

¿Era un día festivo?
```

---

Responder estas preguntas mediante funciones SQL en cada consulta puede ser costoso y generar inconsistencias.

La solución es:

```text
Date Dimension
```

---

# Concepto Fundamental

En lugar de almacenar únicamente una fecha:

```text
2024-01-15
```

almacenamos toda la información relacionada con ella.

---

# Arquitectura

```text
DimDate
      ↓

FactSales
```

---

Todas las Fact Tables utilizan:

```text
DateKey
```

---

# Ejemplo

## DimDate

| DateKey | Date | Day | Month | Quarter | Year |
|----------|------|-----|--------|----------|------|
| 20240115 | 2024-01-15 | 15 | January | Q1 | 2024 |

---

FactSales

| DateKey | ProductKey | SalesAmount |
|----------|------------|-------------|
| 20240115 | 100 | 1500 |

---

Interpretación:

```text
La venta ocurrió
el 15 de enero de 2024.
```

---

# Atributos Comunes

Una Date Dimension suele contener:

```text
Date

Day

Month

Month Number

Quarter

Year

Week

Weekday

Week Number

Day of Year

Is Weekend

Is Holiday
```

---

# Ejemplo Completo

| DateKey | Date | Day | Month | Quarter | Year | Weekday |
|----------|------|-----|--------|----------|------|----------|
| 20240115 | 2024-01-15 | 15 | January | Q1 | 2024 | Monday |

---

# Beneficios

## Consultas más simples

---

En lugar de:

```sql
MONTH(OrderDate)
```

utilizamos:

```sql
d.Month
```

---

## Mejor rendimiento

Evita cálculos repetitivos.

---

## Consistencia

Todas las consultas utilizan las mismas definiciones.

---

## Más información temporal

Permite análisis avanzados.

---

# Jerarquías

Una Date Dimension permite crear jerarquías naturales.

```text
Year
   ↓

Quarter
   ↓

Month
   ↓

Day
```

---

Ejemplo:

```text
Ventas por año

↓

Ventas por trimestre

↓

Ventas por mes

↓

Ventas por día
```

---

# Calendario Fiscal

Muchas empresas utilizan un calendario diferente al calendario tradicional.

Ejemplo:

```text
Fiscal Year

Fiscal Quarter

Fiscal Month
```

---

La Date Dimension puede almacenar ambos calendarios.

---

# Días Especiales

Puede incluir atributos como:

```text
IsHoliday

IsWeekend

BusinessDay

LastDayOfMonth

FirstDayOfMonth
```

---

Ejemplo:

| Date | IsWeekend | IsHoliday |
|------|------------|------------|
| 2024-12-25 | No | Sí |

---

# Caso Real

Empresa Retail.

Pregunta:

```text
¿Cuáles fueron las ventas
durante los fines de semana?
```

---

Consulta:

```sql
SELECT
    SUM(f.SalesAmount)
FROM FactSales f
JOIN DimDate d
    ON f.DateKey = d.DateKey
WHERE d.IsWeekend = 'Yes';
```

---

# Otra Consulta

Pregunta:

```text
Ventas por trimestre.
```

---

SQL:

```sql
SELECT
    d.Quarter,
    SUM(f.SalesAmount)
FROM FactSales f
JOIN DimDate d
    ON f.DateKey = d.DateKey
GROUP BY d.Quarter;
```

---

# ¿Cómo se genera?

La Date Dimension normalmente:

- Se genera una sola vez.
- Contiene un rango amplio de fechas.

Ejemplo:

```text
2010-01-01

↓

2040-12-31
```

---

No depende de sistemas fuente.

---

# DateKey

Existen varias estrategias.

---

## Entero

```text
20240115
```

---

## Surrogate Key

```text
1

2

3
```

---

La más común es:

```text
YYYYMMDD
```

porque facilita lectura y ordenamiento.

---

# Buenas prácticas

## Crear una única Date Dimension

Compartirla entre todas las Fact Tables.

---

## Generar suficientes años

Pensar en datos históricos y futuros.

---

## Agregar atributos útiles

No limitarse a día, mes y año.

---

## Incluir calendario fiscal

Si la empresa lo utiliza.

---

## Documentar cada atributo

Especialmente indicadores como:

```text
IsHoliday

BusinessDay
```

---

# Error común

Muchos principiantes utilizan:

```sql
MONTH()

YEAR()

DATEPART()
```

en todas las consultas.

---

Resultado:

```text
Consultas más complejas

Mayor consumo de recursos

Inconsistencias
```

---

# Error conceptual frecuente

Muchos creen:

```text
La fecha
no necesita
una dimensión.
```

---

Incorrecto.

La Date Dimension es una de las dimensiones más importantes en un Data Warehouse y prácticamente todos los modelos dimensionales la utilizan.

---

# Caso de Entrevista

Pregunta:

```text
¿Por qué utilizar
una Date Dimension
en lugar de la fecha directamente?
```

---

Respuesta:

```text
Porque centraliza todos los atributos temporales,
mejora el rendimiento,
facilita la creación de jerarquías,
permite manejar calendarios fiscales
y garantiza consistencia en el análisis del tiempo.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar una Date Dimension pregúntate:

1. ¿Qué rango de fechas necesito?
2. ¿Utilizaré calendario fiscal?
3. ¿Necesito identificar días festivos?
4. ¿Qué jerarquías usarán los analistas?
5. ¿Qué atributos temporales serán útiles?
6. ¿Todas las Fact Tables compartirán esta dimensión?
7. ¿Cómo mantendré la dimensión en el futuro?

---

# Relación con los siguientes módulos

```text
BUSINESS KEYS
        ↓
DATE DIMENSION
        ↓
JUNK DIMENSIONS
        ↓
BRIDGE TABLES
        ↓
DATA MARTS
```

---

# Resumen

La Date Dimension es una dimensión especializada que proporciona contexto temporal a las Fact Tables.

Características principales:

- Centraliza información del calendario.
- Facilita consultas analíticas.
- Mejora el rendimiento.
- Soporta jerarquías temporales.
- Permite manejar calendarios fiscales y días especiales.

Es una de las dimensiones más reutilizadas y fundamentales en cualquier Data Warehouse moderno.
