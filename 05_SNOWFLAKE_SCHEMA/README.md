# SNOWFLAKE SCHEMA

## Definición

Snowflake Schema es una extensión del Star Schema donde las dimensiones se normalizan en múltiples tablas relacionadas.

Su nombre proviene de su apariencia visual:

```text
        Category
            |
            |

Brand -- Product -- FactSales -- Customer
            |
            |

        Supplier
```

La estructura se parece a un copo de nieve:

```text
Snowflake
```

---

# ¿Por qué existe?

En Star Schema:

```text
DimProduct
```

puede contener:

| Product | Category | Brand |
|----------|-----------|--------|
| Laptop | Electronics | Dell |

---

Si existen miles de productos:

```text
Category
```

y

```text
Brand
```

se repiten constantemente.

---

Snowflake Schema busca:

```text
Reducir redundancia.
```

---

# Evolución desde Star Schema

## Star Schema

```text
DimProduct
```

---

Contiene:

| Product | Category | Brand |
|----------|-----------|--------|
| Laptop | Electronics | Dell |
| Mouse | Electronics | Logitech |

---

Observación:

```text
Electronics
```

aparece repetidamente.

---

# Snowflake Schema

Separar información relacionada.

---

## DimProduct

| ProductKey | ProductName | CategoryKey | BrandKey |
|------------|------------|------------|----------|
| 100 | Laptop | 1 | 10 |

---

## DimCategory

| CategoryKey | CategoryName |
|-------------|--------------|
| 1 | Electronics |

---

## DimBrand

| BrandKey | BrandName |
|----------|-----------|
| 10 | Dell |

---

Resultado:

```text
Menos redundancia.
```

---

# Arquitectura General

## Star Schema

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

## Snowflake Schema

```text
DimCategory
        ↑

DimProduct
        ↓

     FactSales

        ↑

DimCustomer
```

---

Las dimensiones pueden dividirse en varias tablas.

---

# Componentes

## Fact Table

Permanece igual.

---

Ejemplo:

```text
FactSales
```

---

Contiene:

```text
Métricas
+
Claves
```

---

## Dimension Tables

Se normalizan parcialmente.

---

Ejemplo:

```text
DimProduct
      ↓

DimCategory
      ↓

DimDepartment
```

---

# Ejemplo Completo

## FactSales

| DateKey | ProductKey | SalesAmount |
|----------|------------|-------------|
| 1 | 100 | 1500 |

---

## DimProduct

| ProductKey | ProductName | CategoryKey |
|------------|------------|-------------|
| 100 | Laptop | 1 |

---

## DimCategory

| CategoryKey | CategoryName |
|-------------|-------------|
| 1 | Electronics |

---

Interpretación:

```text
Laptop pertenece a Electronics.
```

---

# Beneficios

## Menor redundancia

Menos repetición de datos.

---

## Mayor consistencia

Información centralizada.

---

## Mejor mantenimiento

Cambios realizados en un solo lugar.

---

## Menor almacenamiento

Especialmente en dimensiones grandes.

---

# Desventajas

## Más joins

Las consultas son más complejas.

---

Ejemplo:

```text
FactSales
      ↓

DimProduct
      ↓

DimCategory
```

---

## Menor simplicidad

Más difícil para usuarios de negocio.

---

## Rendimiento potencialmente menor

Más relaciones que resolver.

---

# Comparación Visual

## Star Schema

```text
FactSales
      ↓

DimProduct
```

---

Consulta:

```text
1 Join
```

---

## Snowflake Schema

```text
FactSales
      ↓

DimProduct
      ↓

DimCategory
```

---

Consulta:

```text
2 Joins
```

---

# Comparación General

| Característica | Star Schema | Snowflake Schema |
|---------------|-------------|------------------|
| Normalización | Baja | Mayor |
| Redundancia | Más alta | Más baja |
| Simplicidad | Muy alta | Media |
| Rendimiento | Generalmente mejor | Puede requerir más joins |
| Mantenimiento | Bueno | Excelente |
| Facilidad para BI | Muy alta | Media |

---

# Caso Real

## Retail

Producto:

```text
Laptop
```

---

Categoría:

```text
Electronics
```

---

Departamento:

```text
Technology
```

---

Modelo Snowflake:

```text
DimProduct
      ↓

DimCategory
      ↓

DimDepartment
```

---

Permite reutilizar información.

---

# Cuándo utilizar Snowflake Schema

Recomendado cuando:

```text
Las dimensiones son grandes.

Existe mucha redundancia.

La consistencia es prioridad.
```

---

Ejemplos:

```text
Productos

Ubicaciones

Jerarquías organizacionales
```

---

# Cuándo utilizar Star Schema

Recomendado cuando:

```text
La simplicidad es prioridad.

Se utilizan herramientas BI.

El rendimiento es crítico.
```

---

# Herramientas BI

Power BI:

```text
Prefiere Star Schema.
```

---

Tableau:

```text
Funciona mejor con Star Schema.
```

---

Looker:

```text
Puede trabajar con ambos.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia entre
Star Schema y Snowflake Schema?
```

---

Respuesta:

```text
Star Schema utiliza dimensiones
más desnormalizadas.

Snowflake Schema normaliza
las dimensiones en múltiples tablas
para reducir redundancia y mejorar consistencia.
```

---

# Error común

Muchos principiantes creen:

```text
Snowflake Schema
siempre es mejor.
```

---

Incorrecto.

Más normalización:

```text
No siempre significa
mejor rendimiento.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Snowflake Schema
reemplaza Star Schema.
```

---

Incorrecto.

Ambos son modelos válidos.

---

La elección depende de:

- Volumen
- Rendimiento
- Complejidad
- Mantenimiento

---

# Pensamiento de Data Warehouse

Antes de elegir Snowflake Schema pregúntate:

1. ¿Existe redundancia significativa?
2. ¿Cuántos joins agregaré?
3. ¿Qué tan importante es el rendimiento?
4. ¿Qué herramientas BI utilizaré?
5. ¿Quién consumirá los datos?
6. ¿Las dimensiones tienen jerarquías complejas?
7. ¿La simplicidad o la normalización es más importante?

---

# Relación con los siguientes módulos

```text
STAR SCHEMA
        ↓
SNOWFLAKE SCHEMA
        ↓
FACT TABLES
        ↓
DIMENSION TABLES
        ↓
CONFORMED DIMENSIONS
```

---

# Resumen

Snowflake Schema es una variante del Star Schema donde las dimensiones se normalizan para reducir redundancia.

Características principales:

- Menor redundancia
- Más consistencia
- Más joins
- Mayor complejidad

Comparación:

```text
Star Schema
=
Más simple
Más rápido

Snowflake Schema
=
Más normalizado
Más mantenible
```

Ambos modelos son fundamentales en Data Warehouse Design y deben seleccionarse según las necesidades del negocio y la arquitectura analítica.
