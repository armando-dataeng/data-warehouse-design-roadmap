# AGGREGATE FACT TABLES

## Definición

Una Aggregate Fact Table es una Fact Table que almacena datos previamente resumidos (pre-aggregated) para mejorar el rendimiento de las consultas analíticas.

En lugar de calcular agregaciones sobre millones de registros cada vez que se ejecuta una consulta, los resultados ya se encuentran almacenados.

---

# ¿Por qué existen?

Supongamos una empresa que registra:

```text
50 millones
de ventas por año.
```

---

Pregunta:

```text
¿Cuáles fueron las ventas
por mes?
```

---

Sin una Aggregate Fact Table:

```sql
SELECT
    Month,
    SUM(SalesAmount)
FROM FactSales
GROUP BY Month;
```

---

La base de datos debe recorrer:

```text
50 millones
de registros.
```

---

Resultado:

```text
Consulta lenta.
```

---

# Solución

Crear una tabla con los resultados ya resumidos.

---

Arquitectura:

```text
FactSales
        ↓

Aggregate Process
        ↓

FactSalesMonthly
```

---

# Concepto Fundamental

Una Aggregate Fact Table almacena:

```text
Datos resumidos
```

---

No almacena:

```text
Cada transacción individual.
```

---

# Ejemplo

## FactSales

| DateKey | ProductKey | SalesAmount |
|----------|------------|-------------|
| 1 | 100 | 100 |
| 1 | 101 | 200 |
| 1 | 102 | 300 |

---

Consulta:

```text
Ventas del día.
```

---

Resultado:

```text
600
```

---

Aggregate Fact Table:

## FactSalesDaily

| DateKey | TotalSales |
|----------|------------|
| 1 | 600 |

---

La consulta ahora lee:

```text
1 fila
```

---

En lugar de:

```text
Millones.
```

---

# Arquitectura

```text
Transaction Fact Table
          ↓

Aggregation Process
          ↓

Aggregate Fact Table
```

---

# Niveles de Agregación

## Diario

```text
Ventas por día.
```

---

## Mensual

```text
Ventas por mes.
```

---

## Anual

```text
Ventas por año.
```

---

## Por Categoría

```text
Ventas por categoría.
```

---

## Por Región

```text
Ventas por región.
```

---

# Ejemplo

## FactSales

| Date | Product | Sales |
|------|----------|--------|
| 01/01 | Laptop | 1000 |
| 01/01 | Mouse | 100 |
| 02/01 | Laptop | 900 |

---

Aggregate:

## FactSalesMonthly

| Month | TotalSales |
|--------|------------|
| January | 2000 |

---

# Caso Real

## Dashboard Ejecutivo

Pregunta:

```text
Ventas por año.
```

---

Sin Aggregate Fact Table:

```text
Escanear
100 millones
de registros.
```

---

Con Aggregate Fact Table:

```text
Leer
12 filas.
```

---

Resultado:

```text
Respuesta casi inmediata.
```

---

# Tipos de Agregación

## SUM

```text
Ventas Totales
```

---

## COUNT

```text
Cantidad de pedidos
```

---

## AVG

```text
Venta promedio
```

---

## MIN

```text
Venta mínima
```

---

## MAX

```text
Venta máxima
```

---

# Ejemplo SQL

Consulta original:

```sql
SELECT
    Year,
    SUM(SalesAmount)
FROM FactSales
GROUP BY Year;
```

---

Consulta optimizada:

```sql
SELECT
    Year,
    TotalSales
FROM FactSalesYearly;
```

---

# Beneficios

## Mejor rendimiento

Consultas mucho más rápidas.

---

## Menor consumo de recursos

Reduce CPU y memoria.

---

## Mejor experiencia para usuarios

Dashboards responden más rápido.

---

## Escalabilidad

Ideal para grandes volúmenes.

---

# Desventajas

## Mayor almacenamiento

Se duplican datos resumidos.

---

## Mantenimiento adicional

Las agregaciones deben actualizarse.

---

## Riesgo de inconsistencias

Si no se sincronizan correctamente.

---

# Caso Real

## Empresa Retail

FactSales:

```text
500 millones
de registros.
```

---

Power BI consulta:

```text
Ventas por mes.
```

---

Solución:

```text
FactSalesMonthly
```

---

Resultado:

```text
Dashboard carga
en segundos.
```

---

# Aggregate Fact Table vs Transaction Fact Table

| Característica | Transaction Fact | Aggregate Fact |
|---------------|------------------|----------------|
| Nivel de detalle | Máximo | Resumido |
| Granularidad | Baja | Alta |
| Rendimiento | Menor | Mayor |
| Tamaño | Grande | Pequeño |
| Uso | Análisis detallado | Dashboards y KPIs |

---

# Cuándo utilizar Aggregate Fact Tables

Cuando:

```text
Las consultas
repiten constantemente
las mismas agregaciones.
```

---

Ejemplos:

```text
Ventas mensuales

Ventas anuales

KPIs ejecutivos

Dashboards
```

---

# Cuándo NO utilizarlas

Si:

```text
El volumen es pequeño.
```

---

O si:

```text
Las consultas
cambian constantemente.
```

---

# Buenas prácticas

## Mantener una Fact Table detallada

Nunca reemplazar la tabla transaccional.

---

## Crear agregaciones según necesidades del negocio

No agregar por agregar.

---

## Automatizar la actualización

Mantener datos sincronizados.

---

## Documentar el nivel de agregación

Definir claramente el grain.

---

## Medir el beneficio

Crear agregados solo cuando mejoren el rendimiento.

---

# Error común

Muchos equipos crean:

```text
Demasiadas
Aggregate Fact Tables.
```

---

Resultado:

```text
Mayor mantenimiento.

Duplicación innecesaria.

Mayor costo.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Aggregate Fact Table
reemplaza
Fact Table.
```

---

Incorrecto.

La Aggregate Fact Table:

```text
Complementa
```

a la Fact Table transaccional.

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es una Aggregate Fact Table?
```

---

Respuesta:

```text
Es una Fact Table que almacena datos previamente resumidos para mejorar el rendimiento de consultas analíticas frecuentes, evitando recalcular agregaciones sobre grandes volúmenes de datos.
```

---

# Pensamiento de Data Warehouse

Antes de crear una Aggregate Fact Table pregúntate:

1. ¿Qué consultas se ejecutan con mayor frecuencia?
2. ¿Cuál es el nivel de agregación adecuado?
3. ¿Cuánto mejorará el rendimiento?
4. ¿Cómo actualizaré los datos?
5. ¿Qué impacto tendrá en el almacenamiento?
6. ¿La agregación seguirá siendo útil en el futuro?
7. ¿Realmente necesito una tabla agregada?

---

# Relación con los siguientes módulos

```text
FACTLESS FACT TABLES
        ↓
AGGREGATE FACT TABLES
        ↓
SLOWLY CHANGING DIMENSIONS
        ↓
SURROGATE KEYS
```

---

# Resumen

Las Aggregate Fact Tables almacenan datos previamente resumidos para acelerar consultas analíticas.

Características principales:

- Datos preagregados.
- Mejor rendimiento.
- Menor consumo de recursos.
- Ideales para dashboards y KPIs.

Casos de uso:

- Ventas por mes.
- Ventas por año.
- Reportes ejecutivos.
- Indicadores de negocio.

Son una técnica clásica de optimización en Data Warehousing y Business Intelligence, especialmente útil cuando se trabaja con grandes volúmenes de datos.
