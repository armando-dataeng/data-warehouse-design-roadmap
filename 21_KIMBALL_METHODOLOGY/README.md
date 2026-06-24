# KIMBALL METHODOLOGY

## Definición

La Metodología Kimball es un enfoque para diseñar e implementar Data Warehouses basado en el modelado dimensional.

Fue propuesta por Ralph Kimball y se caracteriza por construir Data Marts orientados al negocio que, mediante dimensiones conformadas, forman un Enterprise Data Warehouse.

Es uno de los enfoques más utilizados en proyectos de Business Intelligence y Analytics.

---

# ¿Quién fue Ralph Kimball?

Ralph Kimball es uno de los principales referentes en Data Warehousing.

Es autor de:

```text
The Data Warehouse Toolkit
```

---

Su metodología introdujo conceptos como:

```text
Star Schema

Fact Tables

Dimension Tables

Conformed Dimensions

Slowly Changing Dimensions

Junk Dimensions

Bridge Tables
```

---

Gran parte del modelado dimensional moderno proviene de su trabajo.

---

# Filosofía

Kimball propone:

```text
Construir primero
los Data Marts.

↓

Integrarlos

↓

Formar el Enterprise Data Warehouse.
```

---

Este enfoque se conoce como:

```text
Bottom-Up.
```

---

# Arquitectura

```text
Operational Systems

        ↓

ETL / ELT

        ↓

Business Process

        ↓

Data Mart

        ↓

Conformed Dimensions

        ↓

Enterprise Data Warehouse
```

---

Cada nuevo Data Mart amplía la solución empresarial.

---

# Principios Fundamentales

## Orientado al negocio

El diseño comienza identificando:

```text
Procesos del negocio.
```

---

Ejemplos:

```text
Ventas

Compras

Inventario

Pagos

Facturación
```

---

## Modelado Dimensional

Utiliza:

```text
Fact Tables

↓

Dimension Tables
```

---

Generalmente mediante:

```text
Star Schema.
```

---

## Conformed Dimensions

Permiten compartir dimensiones entre Data Marts.

---

Ejemplo:

```text
DimCustomer

↓

Sales Mart

Finance Mart
```

---

Resultado:

```text
KPIs consistentes.
```

---

# Ciclo de Diseño

## Paso 1

Seleccionar el proceso del negocio.

---

Ejemplo:

```text
Ventas.
```

---

## Paso 2

Definir el Grain.

---

Pregunta:

```text
¿Qué representa
una fila?
```

---

## Paso 3

Identificar dimensiones.

---

Ejemplo:

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

Ejemplo:

```text
Cantidad

Ventas

Ganancia
```

---

## Paso 5

Diseñar el Star Schema.

---

Resultado:

```text
FactSales

↓

DimCustomer

DimProduct

DimDate

DimStore
```

---

# Bus Matrix

Una herramienta característica de Kimball.

---

La Bus Matrix relaciona:

```text
Procesos del negocio

↓

Dimensiones conformadas
```

---

Ejemplo:

| Business Process | Customer | Product | Date | Store |
|------------------|----------|----------|------|--------|
| Sales | ✓ | ✓ | ✓ | ✓ |
| Returns | ✓ | ✓ | ✓ | ✓ |
| Inventory | | ✓ | ✓ | ✓ |

---

Permite identificar:

```text
Dimensiones compartidas.
```

---

# Ventajas

## Desarrollo incremental

Cada Data Mart agrega valor.

---

## Resultados rápidos

Los usuarios obtienen información desde las primeras fases.

---

## Modelos simples

Star Schema.

---

## Excelente rendimiento

Optimizado para BI.

---

## Fácil comprensión

Ideal para analistas.

---

# Desventajas

## Requiere buena gobernanza

Las dimensiones compartidas deben mantenerse consistentes.

---

## Integración

Debe planificarse cuidadosamente.

---

## Riesgo de duplicación

Si no se diseñan correctamente las dimensiones conformadas.

---

# Caso Real

Empresa Retail.

Fase 1:

```text
Sales Mart
```

---

Fase 2:

```text
Inventory Mart
```

---

Fase 3:

```text
Finance Mart
```

---

Todos utilizan:

```text
DimCustomer

DimProduct

DimDate
```

---

Finalmente:

```text
Enterprise Data Warehouse.
```

---

# Kimball vs Inmon

Kimball:

```text
Data Marts

↓

Enterprise Data Warehouse
```

---

Inmon:

```text
Enterprise Data Warehouse

↓

Data Marts
```

---

Kimball:

```text
Bottom-Up
```

---

Inmon:

```text
Top-Down
```

---

# Casos de Uso

Kimball es ideal cuando:

- Se necesitan resultados rápidos.
- El negocio requiere dashboards cuanto antes.
- Se trabaja con metodologías ágiles.
- Se construyen soluciones de BI incrementales.

---

# Buenas prácticas

## Diseñar por procesos

No por sistemas.

---

## Definir correctamente el Grain

Es la decisión más importante del modelo.

---

## Reutilizar dimensiones

Mediante Conformed Dimensions.

---

## Priorizar Star Schema

Facilita el análisis.

---

## Documentar reglas de negocio

Garantiza consistencia.

---

# Error común

Muchos equipos crean:

```text
Data Marts

↓

Sin dimensiones compartidas.
```

---

Resultado:

```text
KPIs inconsistentes.

Duplicación.

Problemas de integración.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Kimball

=

Solo Star Schema.
```

---

Incorrecto.

Kimball es:

```text
Una metodología completa
para construir
Data Warehouses.
```

---

El Star Schema es solo uno de sus componentes.

---

# Caso de Entrevista

Pregunta:

```text
¿Qué propone
la metodología Kimball?
```

---

Respuesta:

```text
Kimball propone construir Data Marts orientados a procesos del negocio utilizando modelado dimensional y dimensiones conformadas. Con el tiempo, estos Data Marts se integran para formar un Enterprise Data Warehouse mediante un enfoque Bottom-Up.
```

---

# Pensamiento de Arquitectura

Antes de aplicar Kimball pregúntate:

1. ¿Cuál es el proceso de negocio más importante?
2. ¿Qué Data Mart aportará mayor valor?
3. ¿Qué dimensiones podrán compartirse?
4. ¿Cuál será el Grain?
5. ¿Cómo garantizaré KPIs consistentes?
6. ¿Cómo crecerá la arquitectura?
7. ¿Cómo integraré futuros Data Marts?

---

# Relación con los siguientes módulos

```text
ENTERPRISE DATA WAREHOUSE
        ↓
KIMBALL METHODOLOGY
        ↓
INMON METHODOLOGY
        ↓
DATA WAREHOUSE CASE STUDY
```

---

# Resumen

La Metodología Kimball es un enfoque Bottom-Up para construir Data Warehouses mediante modelado dimensional.

Principios principales:

- Orientación a procesos del negocio.
- Desarrollo incremental.
- Star Schema.
- Fact Tables.
- Dimension Tables.
- Conformed Dimensions.
- Bus Matrix.

Su objetivo es entregar valor rápidamente mediante Data Marts integrados que evolucionan hasta formar un Enterprise Data Warehouse consistente, escalable y optimizado para el análisis.
