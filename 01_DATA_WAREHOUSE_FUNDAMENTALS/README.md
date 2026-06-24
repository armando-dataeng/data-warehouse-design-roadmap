# DATA WAREHOUSE FUNDAMENTALS

## Definición

Un Data Warehouse es un repositorio centralizado diseñado para almacenar datos históricos provenientes de múltiples fuentes con fines analíticos.

Su objetivo principal es:

```text
Convertir datos operacionales
en información útil para la toma de decisiones.
```

---

# ¿Por qué existe un Data Warehouse?

Las empresas tienen datos en muchos sistemas:

```text
ERP
CRM
E-commerce
Aplicaciones móviles
APIs
Archivos
```

Cada sistema responde preguntas operacionales.

Pero la empresa necesita responder preguntas estratégicas:

```text
¿Cuánto vendimos este año?

¿Cuál es el cliente más rentable?

¿Qué producto genera más ingresos?

¿Qué región está creciendo más?
```

Para eso existe un Data Warehouse.

---

# Data Warehouse vs Base de Datos Operacional

## Base de Datos Operacional

Diseñada para registrar operaciones.

Ejemplos:

```text
Crear pedido
Actualizar cliente
Registrar pago
Procesar transferencia
```

---

## Data Warehouse

Diseñado para análisis.

Ejemplos:

```text
Ventas por mes
Clientes por segmento
Ingresos por región
Tendencias históricas
```

---

# Características Principales

## Orientado al negocio

Los datos se organizan alrededor de procesos importantes:

```text
Ventas
Clientes
Inventario
Pagos
Transacciones
```

---

## Integrado

Combina datos de múltiples fuentes.

---

## Histórico

Almacena información durante largos períodos.

Ejemplo:

```text
Datos de 5 años
Datos de 10 años
```

---

## No volátil

Los datos normalmente se cargan y se consultan.

No se modifican constantemente como en sistemas OLTP.

---

# Arquitectura General

```text
Sistemas Fuente
        ↓

ETL / ELT
        ↓

Data Warehouse
        ↓

BI / Analytics
```

---

# Componentes Principales

## Sistemas Fuente

Origen de los datos.

Ejemplos:

```text
SQL Server
PostgreSQL
Salesforce
SAP
Stripe
Archivos CSV
```

---

## ETL / ELT

Procesos para mover y transformar datos.

```text
Extract
Transform
Load
```

o

```text
Extract
Load
Transform
```

---

## Data Warehouse

Repositorio central analítico.

---

## BI Tools

Herramientas de visualización.

Ejemplos:

```text
Power BI
Tableau
Looker
Excel
```

---

# Caso Real

## Empresa Retail

Fuentes:

```text
E-commerce
ERP
CRM
Sistema de pagos
```

---

Data Warehouse:

```text
FactVentas
DimCliente
DimProducto
DimFecha
```

---

Preguntas que responde:

```text
Ventas por mes
Productos más vendidos
Clientes más rentables
Ingresos por región
```

---

# OLTP vs Data Warehouse

| Característica | OLTP | Data Warehouse |
|---------------|------|----------------|
| Objetivo | Operaciones | Análisis |
| Datos | Actuales | Históricos |
| Consultas | Cortas | Complejas |
| Usuarios | Aplicaciones | Analistas |
| Modelo | Normalizado | Dimensional |
| Escrituras | Frecuentes | Controladas |
| Lecturas | Individuales | Masivas |

---

# Modelado Dimensional

El Data Warehouse suele utilizar:

```text
Star Schema
Snowflake Schema
```

---

Componentes:

```text
Fact Tables
Dimension Tables
```

---

# Fact Tables

Almacenan métricas.

Ejemplos:

```text
Ventas
Cantidad
Monto
Costo
Ganancia
```

---

# Dimension Tables

Almacenan contexto.

Ejemplos:

```text
Cliente
Producto
Fecha
Sucursal
Región
```

---

# Ejemplo Simple

## FactVentas

| FechaKey | ProductoKey | ClienteKey | Ventas |
|----------|-------------|------------|--------|
| 1 | 100 | 10 | 1500 |

---

## DimProducto

| ProductoKey | Producto |
|-------------|----------|
| 100 | Laptop |

---

## DimCliente

| ClienteKey | Cliente |
|------------|---------|
| 10 | Pedro |

---

Interpretación:

```text
Pedro compró una Laptop por 1500.
```

---

# Beneficios

## Mejor análisis

Permite responder preguntas estratégicas.

---

## Mejor rendimiento

Optimizado para consultas analíticas.

---

## Fuente única de verdad

Centraliza información empresarial.

---

## Datos históricos

Permite analizar tendencias.

---

## Integración

Unifica datos de múltiples sistemas.

---

# Desafíos

## Calidad de datos

Los datos fuente pueden contener errores.

---

## Integración compleja

Muchas fuentes tienen formatos diferentes.

---

## Costos

Infraestructura, almacenamiento y procesamiento.

---

## Gobierno de datos

Control de accesos, definiciones y responsabilidades.

---

# Error común

Muchos principiantes creen:

```text
Data Warehouse = Base de datos grande
```

Incorrecto.

Un Data Warehouse no se define solo por tamaño.

Se define por su propósito:

```text
Análisis histórico y toma de decisiones.
```

---

# Error conceptual frecuente

Muchos creen que un Data Warehouse reemplaza al sistema operacional.

Incorrecto.

El sistema operacional registra operaciones.

El Data Warehouse analiza operaciones.

---

# Pensamiento de Data Engineering

Antes de diseñar un Data Warehouse pregúntate:

1. ¿Qué preguntas de negocio debe responder?
2. ¿Cuáles son las fuentes de datos?
3. ¿Qué datos históricos necesito conservar?
4. ¿Qué métricas analizaré?
5. ¿Qué dimensiones darán contexto?
6. ¿Qué nivel de calidad requiere el negocio?
7. ¿Quién consumirá los datos?

---

# Relación con los siguientes módulos

```text
DATA WAREHOUSE FUNDAMENTALS
        ↓
OLTP VS OLAP
        ↓
DIMENSIONAL MODELING
        ↓
STAR SCHEMA
        ↓
FACT TABLES
        ↓
DIMENSION TABLES
```

---

# Resumen

Un Data Warehouse es una plataforma diseñada para análisis empresarial.

Características principales:

- Centraliza datos.
- Integra múltiples fuentes.
- Conserva históricos.
- Optimiza consultas analíticas.
- Soporta BI y toma de decisiones.

Es uno de los pilares fundamentales de Data Engineering, Business Intelligence y Analytics Engineering.
