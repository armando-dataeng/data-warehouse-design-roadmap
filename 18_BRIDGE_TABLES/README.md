# BRIDGE TABLES

## Definición

Una Bridge Table es una tabla utilizada en un modelo dimensional para representar relaciones muchos a muchos (Many-to-Many) entre una Fact Table y una Dimension Table, o entre dos dimensiones.

Su objetivo es mantener el modelo flexible sin duplicar datos ni romper la integridad del diseño.

---

# ¿Por qué existen?

La mayoría de los modelos dimensionales asumen relaciones:

```text
Uno a Muchos (1:N)
```

Ejemplo:

```text
Un Cliente

↓

Muchas Ventas
```

---

Pero algunos procesos del negocio presentan relaciones:

```text
Muchos a Muchos (M:N)
```

---

Ejemplos:

```text
Un empleado trabaja
en varios proyectos.

↓

Un proyecto tiene
muchos empleados.
```

---

O:

```text
Un producto tiene
varias promociones.

↓

Una promoción aplica
a muchos productos.
```

---

Estas relaciones no pueden modelarse directamente en un Star Schema.

---

# Solución

Agregar una:

```text
Bridge Table.
```

---

# Arquitectura

Sin Bridge Table:

```text
FactSales

↓

DimPromotion
```

---

Problema:

```text
Una venta

↓

Puede tener

↓

Varias promociones.
```

---

Con Bridge Table:

```text
DimPromotion

      ↑

BridgePromotion

      ↓

FactSales
```

---

Ahora:

```text
Una venta

↓

Puede relacionarse

↓

Con múltiples promociones.
```

---

# Ejemplo

Supongamos:

Venta:

```text
Venta #100
```

---

Promociones:

```text
Black Friday

Cupón

Cliente Premium
```

---

FactSales

| SalesKey | SalesAmount |
|-----------|-------------|
| 100 | 1500 |

---

DimPromotion

| PromotionKey | PromotionName |
|--------------|---------------|
| 1 | Black Friday |
| 2 | Coupon |
| 3 | Premium Customer |

---

BridgePromotion

| SalesKey | PromotionKey |
|-----------|--------------|
| 100 | 1 |
| 100 | 2 |
| 100 | 3 |

---

Resultado:

```text
Una venta

↓

Tres promociones.
```

---

# Otro Ejemplo

Empresa de Consultoría.

Empleado:

```text
Pedro
```

Trabaja en:

```text
Proyecto A

Proyecto B

Proyecto C
```

---

Proyecto A tiene:

```text
Pedro

Ana

Luis
```

---

Modelo:

```text
DimEmployee

↓

BridgeEmployeeProject

↓

DimProject
```

---

# Ejemplo Médico

Paciente:

```text
Juan
```

---

Diagnósticos:

```text
Diabetes

Hipertensión

Obesidad
```

---

Modelo:

```text
DimPatient

↓

BridgePatientDiagnosis

↓

DimDiagnosis
```

---

# Arquitectura General

```text
Dimension A

      ↑

Bridge Table

      ↓

Dimension B
```

---

O:

```text
Dimension

      ↑

Bridge Table

      ↓

Fact Table
```

---

# Weighting Factor

En algunos casos una Bridge Table incluye una columna:

```text
Weight
```

---

Ejemplo:

| SalesKey | PromotionKey | Weight |
|-----------|--------------|---------|
| 100 | 1 | 0.5 |
| 100 | 2 | 0.3 |
| 100 | 3 | 0.2 |

---

Permite distribuir métricas correctamente.

---

Muy utilizado cuando:

```text
Una venta

↓

Debe repartirse

↓

Entre varias categorías.
```

---

# Beneficios

## Modela relaciones M:N

---

## Evita duplicar registros

---

## Mantiene integridad

---

## Mayor flexibilidad

---

## Compatible con Star Schema

---

# Desventajas

## Consultas más complejas

Más JOINs.

---

## Mayor mantenimiento

---

## Riesgo de doble conteo

Si no se diseñan correctamente las consultas.

---

# Caso Real

Empresa de Seguros.

Cliente:

```text
Puede tener

↓

Varios beneficiarios.
```

---

Beneficiario:

```text
Puede pertenecer

↓

A varias pólizas.
```

---

Bridge Table:

```text
BridgePolicyBeneficiary
```

---

# Cuándo utilizar Bridge Tables

Cuando existe una relación:

```text
Muchos a Muchos.
```

---

Ejemplos:

- Productos y promociones.
- Empleados y proyectos.
- Pacientes y diagnósticos.
- Estudiantes y cursos.
- Clientes y campañas.

---

# Cuándo NO utilizarlas

Si la relación es:

```text
Uno a Muchos.
```

---

Ejemplo:

```text
Cliente

↓

Pedidos
```

---

No se necesita una Bridge Table.

---

# Buenas prácticas

## Confirmar que realmente existe una relación M:N

No utilizarlas por costumbre.

---

## Documentar claramente la relación

Especialmente si existe una columna Weight.

---

## Evitar doble conteo

Diseñar consultas cuidadosamente.

---

## Utilizar Surrogate Keys

Mantener consistencia.

---

## Validar el impacto en el rendimiento

Cada JOIN adicional tiene un costo.

---

# Error común

Muchos principiantes duplican registros en la Fact Table.

Ejemplo:

```text
Venta 100

↓

Promoción A

↓

Venta duplicada

↓

Promoción B

↓

Venta duplicada
```

---

Resultado:

```text
Ventas incorrectas.

KPIs inflados.
```

---

La solución correcta es:

```text
Bridge Table.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Bridge Table

=

Tabla puente
entre cualquier tabla.
```

---

Incorrecto.

Su objetivo principal es resolver:

```text
Relaciones

Muchos a Muchos.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Cuándo utilizarías
una Bridge Table?
```

---

Respuesta:

```text
Cuando existe una relación muchos a muchos entre dimensiones o entre una Fact Table y una dimensión, y es necesario modelarla sin duplicar registros ni perder integridad en el modelo dimensional.
```

---

# Pensamiento de Data Warehouse

Antes de crear una Bridge Table pregúntate:

1. ¿Existe realmente una relación muchos a muchos?
2. ¿Puedo resolverla con un modelo más simple?
3. ¿Existe riesgo de doble conteo?
4. ¿Necesito una columna Weight?
5. ¿Cómo afectará el rendimiento?
6. ¿Las consultas seguirán siendo comprensibles?
7. ¿La solución refleja correctamente el negocio?

---

# Relación con los siguientes módulos

```text
JUNK DIMENSIONS
        ↓
BRIDGE TABLES
        ↓
DATA MARTS
        ↓
KIMBALL METHODOLOGY
        ↓
INMON METHODOLOGY
```

---

# Resumen

Las Bridge Tables permiten modelar relaciones muchos a muchos en un Data Warehouse.

Características principales:

- Resuelven relaciones M:N.
- Evitan duplicar registros.
- Mantienen la integridad del modelo.
- Permiten escenarios complejos del negocio.
- Pueden incluir factores de ponderación (Weight).

Casos comunes:

- Productos y promociones.
- Empleados y proyectos.
- Pacientes y diagnósticos.
- Estudiantes y cursos.
- Clientes y campañas.

Son un patrón avanzado del modelado dimensional y una herramienta fundamental para representar relaciones complejas en Data Warehouses empresariales.
