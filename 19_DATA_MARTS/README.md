# DATA MARTS

## Definición

Un Data Mart es un subconjunto de un Data Warehouse diseñado para satisfacer las necesidades analíticas de un área específica del negocio.

Su objetivo es proporcionar datos relevantes y optimizados para un departamento, equipo o proceso empresarial.

---

# ¿Por qué existen?

Supongamos una empresa con las siguientes áreas:

```text
Ventas

Marketing

Finanzas

Recursos Humanos

Operaciones
```

---

Pregunta:

```text
¿Todos los departamentos
necesitan acceder
a todo el Data Warehouse?
```

---

Respuesta:

```text
No.
```

---

Cada área necesita únicamente los datos relacionados con su trabajo.

---

La solución es:

```text
Data Marts.
```

---

# Concepto Fundamental

Un Data Mart contiene:

```text
Información específica

↓

Para un área del negocio.
```

---

Ejemplos:

```text
Sales Data Mart

Marketing Data Mart

Finance Data Mart

HR Data Mart
```

---

# Arquitectura

```text
Operational Systems
          ↓

ETL / ELT
          ↓

Enterprise Data Warehouse
          ↓
   ┌──────┼──────┐
   │      │      │
Sales   Finance  HR
Mart     Mart    Mart
```

---

Todos los Data Marts provienen del mismo Data Warehouse.

---

# Ejemplo

Empresa Retail.

Data Warehouse:

```text
Clientes

Productos

Ventas

Inventario

Empleados

Pagos
```

---

Sales Mart

```text
Clientes

Productos

Ventas
```

---

Finance Mart

```text
Ventas

Pagos

Costos

Ganancias
```

---

HR Mart

```text
Empleados

Departamentos

Salarios
```

---

Cada equipo consulta únicamente la información que necesita.

---

# Tipos de Data Marts

## Dependent Data Mart

Obtiene sus datos desde:

```text
Enterprise Data Warehouse.
```

---

Arquitectura:

```text
Operational Systems

↓

Data Warehouse

↓

Data Mart
```

---

Es el tipo más recomendado.

---

## Independent Data Mart

Obtiene datos directamente desde los sistemas operacionales.

---

Arquitectura:

```text
Operational Systems

↓

Data Mart
```

---

Problema:

```text
Duplicación

Inconsistencia

Mayor mantenimiento
```

---

## Hybrid Data Mart

Combina datos provenientes del:

```text
Data Warehouse

+

Sistemas Operacionales
```

---

Se utiliza en escenarios específicos.

---

# Caso Real

Empresa de E-commerce.

## Sales Mart

KPIs:

```text
Ventas

Ingresos

Productos

Clientes
```

---

## Marketing Mart

KPIs:

```text
Campañas

Conversión

Canales

Leads
```

---

## Finance Mart

KPIs:

```text
Ingresos

Costos

Rentabilidad
```

---

Todos provienen del mismo:

```text
Enterprise Data Warehouse.
```

---

# Beneficios

## Mejor rendimiento

Consultas sobre menos datos.

---

## Mayor seguridad

Cada área accede solo a su información.

---

## Facilidad de uso

Modelos adaptados al negocio.

---

## Menor complejidad

Los usuarios no necesitan conocer todo el Data Warehouse.

---

## Escalabilidad

Cada Data Mart puede evolucionar independientemente.

---

# Data Warehouse vs Data Mart

| Característica | Data Warehouse | Data Mart |
|---------------|----------------|-----------|
| Alcance | Toda la empresa | Un área específica |
| Usuarios | Organización completa | Departamento |
| Datos | Integrados | Especializados |
| Tamaño | Mayor | Menor |
| Objetivo | Centralizar información | Facilitar análisis específicos |

---

# Arquitectura Empresarial

```text
CRM
ERP
E-commerce
      ↓

ETL / ELT
      ↓

Enterprise Data Warehouse
      ↓
 ┌────┼─────┬─────┐
 │    │     │     │
Sales Finance HR Marketing
Mart   Mart  Mart Mart
```

---

# Star Schema dentro de un Data Mart

Ejemplo:

Sales Mart

```text
FactSales
      ↓

DimCustomer

DimProduct

DimDate

DimStore
```

---

Cada Data Mart puede tener su propio modelo dimensional.

---

# Relación con Conformed Dimensions

Las dimensiones compartidas permiten que distintos Data Marts utilicen la misma definición de entidades.

Ejemplo:

```text
Sales Mart

↓

DimCustomer

↑

Finance Mart
```

---

Resultado:

```text
KPIs consistentes
en toda la empresa.
```

---

# Buenas prácticas

## Diseñar primero el Enterprise Data Warehouse

Luego construir los Data Marts.

---

## Compartir dimensiones comunes

Cliente

Producto

Fecha

Ubicación

---

## Evitar duplicar lógica

Centralizar reglas de negocio.

---

## Mantener modelos simples

Pensar en el usuario final.

---

## Documentar KPIs

Todos deben compartir las mismas definiciones.

---

# Error común

Muchos equipos crean:

```text
Un Data Mart

↓

Por cada proyecto.
```

---

Resultado:

```text
Duplicación

Inconsistencia

Múltiples versiones
de la verdad.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Data Mart

=

Base de datos pequeña.
```

---

Incorrecto.

Un Data Mart es:

```text
Un modelo analítico

orientado

a un dominio

del negocio.
```

---

Puede contener millones de registros.

---

# Caso de Entrevista

Pregunta:

```text
¿Cuál es la diferencia
entre un Data Warehouse
y un Data Mart?
```

---

Respuesta:

```text
El Data Warehouse integra información de toda la organización.

Un Data Mart es un subconjunto orientado a un área específica del negocio, diseñado para facilitar consultas y análisis especializados.
```

---

# Pensamiento de Data Warehouse

Antes de crear un Data Mart pregúntate:

1. ¿Qué área del negocio lo utilizará?
2. ¿Qué KPIs necesita?
3. ¿Qué dimensiones compartirá con otros Data Marts?
4. ¿Qué nivel de detalle requiere?
5. ¿Cómo garantizaré consistencia?
6. ¿Qué usuarios consumirán la información?
7. ¿Cómo evolucionará con el tiempo?

---

# Relación con los siguientes módulos

```text
BRIDGE TABLES
        ↓
DATA MARTS
        ↓
KIMBALL METHODOLOGY
        ↓
INMON METHODOLOGY
        ↓
DATA WAREHOUSE CASE STUDY
```

---

# Resumen

Los Data Marts son subconjuntos especializados de un Data Warehouse diseñados para satisfacer las necesidades analíticas de áreas específicas del negocio.

Tipos principales:

- Dependent Data Mart
- Independent Data Mart
- Hybrid Data Mart

Beneficios:

- Mejor rendimiento.
- Mayor seguridad.
- Modelos más simples.
- Escalabilidad.
- Experiencia analítica optimizada.

Los Data Marts permiten acercar la información correcta a los usuarios adecuados, manteniendo una arquitectura empresarial consistente y escalable.
