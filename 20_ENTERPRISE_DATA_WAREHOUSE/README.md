# ENTERPRISE DATA WAREHOUSE (EDW)

## Definición

Un Enterprise Data Warehouse (EDW) es un repositorio centralizado que integra datos provenientes de toda la organización para proporcionar una visión única, consistente e histórica del negocio.

Su objetivo es convertirse en la fuente única de verdad (Single Source of Truth) para la toma de decisiones.

---

# ¿Por qué existe?

Una empresa puede tener múltiples sistemas:

```text
CRM

ERP

E-commerce

POS

Recursos Humanos

Finanzas
```

---

Cada sistema contiene una parte de la información.

---

Pregunta:

```text
¿Cómo obtenemos
una visión completa
del negocio?
```

---

Respuesta:

```text
Enterprise Data Warehouse.
```

---

# Concepto Fundamental

Un EDW integra información de:

```text
Todas las áreas

↓

En un único repositorio.
```

---

No pertenece a un departamento específico.

---

Representa:

```text
Toda la organización.
```

---

# Arquitectura General

```text
CRM

ERP

E-commerce

Finance

HR

POS

        ↓

      ETL / ELT

        ↓

Enterprise Data Warehouse

        ↓

Data Marts

        ↓

Power BI
Tableau
Looker
```

---

# Objetivos

Un EDW busca:

- Integrar datos.
- Eliminar silos.
- Garantizar consistencia.
- Conservar historial.
- Facilitar el análisis empresarial.

---

# Características

## Centralizado

Toda la información vive en un único repositorio.

---

## Integrado

Combina múltiples sistemas.

---

## Histórico

Conserva información durante años.

---

## Orientado al análisis

Optimizado para consultas analíticas.

---

## No Volátil

Los datos normalmente se cargan y consultan.

No se modifican continuamente como en un sistema OLTP.

---

# Ejemplo

Empresa Retail.

Fuentes:

```text
ERP

CRM

E-commerce

Sistema de Inventario
```

---

Enterprise Data Warehouse:

```text
DimCustomer

DimProduct

DimStore

DimDate

FactSales

FactInventory
```

---

Pregunta:

```text
¿Cuál fue
la rentabilidad

por producto

durante los últimos
cinco años?
```

---

El EDW puede responderla porque:

```text
Integra toda
la información.
```

---

# Data Warehouse vs Enterprise Data Warehouse

## Data Warehouse

Puede referirse a cualquier repositorio analítico.

---

## Enterprise Data Warehouse

Integra:

```text
Toda la organización.
```

---

Su alcance es empresarial.

---

# EDW vs Data Mart

## Enterprise Data Warehouse

```text
Información global.
```

---

Ejemplo:

```text
Ventas

Finanzas

Marketing

RRHH

Operaciones
```

---

## Data Mart

```text
Información específica.
```

---

Ejemplo:

```text
Solo Ventas.
```

---

# Arquitectura Empresarial

```text
Operational Systems

        ↓

Raw Layer

        ↓

Staging

        ↓

Enterprise Data Warehouse

        ↓

Sales Mart

Finance Mart

Marketing Mart
```

---

# Componentes

## Data Sources

Origen de datos.

---

## ETL / ELT

Integración.

---

## Enterprise Data Warehouse

Repositorio central.

---

## Data Marts

Modelos específicos.

---

## BI Tools

Consumo.

---

# Beneficios

## Fuente única de verdad

Todos utilizan los mismos datos.

---

## Consistencia

Mismos KPIs.

---

## Integración

Elimina silos.

---

## Escalabilidad

Permite crecer con la empresa.

---

## Gobierno de datos

Facilita seguridad y calidad.

---

# Caso Real

Empresa multinacional.

Sistemas:

```text
SAP

Salesforce

Oracle

Workday

Shopify
```

---

Cada país utiliza aplicaciones distintas.

---

El EDW integra toda la información.

---

Ahora la dirección puede consultar:

```text
Ventas globales

Rentabilidad

Inventario

Clientes

Finanzas
```

---

# Desafíos

## Integración

Muchos sistemas.

---

## Calidad de datos

Datos inconsistentes.

---

## Gobernanza

Definir estándares.

---

## Costos

Infraestructura.

---

## Mantenimiento

Procesos continuos.

---

# Buenas prácticas

## Diseñar un modelo empresarial

Pensar en toda la organización.

---

## Compartir dimensiones

Cliente

Producto

Fecha

Ubicación

---

## Definir estándares

KPIs

Nombres

Reglas

---

## Automatizar cargas

Reducir procesos manuales.

---

## Documentar todo

Facilitar evolución.

---

# Error común

Muchos equipos crean:

```text
Un Data Warehouse

↓

Por departamento.
```

---

Resultado:

```text
Silos.

Duplicación.

KPIs inconsistentes.
```

---

La solución es:

```text
Enterprise Data Warehouse

↓

Data Marts.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Enterprise Data Warehouse

=

Base de datos enorme.
```

---

Incorrecto.

Un EDW es:

```text
Una arquitectura empresarial
para integrar datos
de toda la organización.
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es un
Enterprise Data Warehouse?
```

---

Respuesta:

```text
Es un repositorio centralizado que integra datos provenientes de múltiples sistemas y áreas del negocio para proporcionar una visión única, consistente e histórica de la organización y servir como fuente principal para el análisis y la toma de decisiones.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar un Enterprise Data Warehouse pregúntate:

1. ¿Qué sistemas debo integrar?
2. ¿Qué procesos de negocio cubriré?
3. ¿Qué dimensiones compartirán los Data Marts?
4. ¿Cómo garantizaré una única versión de la verdad?
5. ¿Qué estrategia de integración utilizaré?
6. ¿Cómo escalará la plataforma?
7. ¿Cómo aseguraré la calidad y gobernanza de los datos?

---

# Relación con los siguientes módulos

```text
DATA MARTS
        ↓
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

Un Enterprise Data Warehouse (EDW) es el repositorio analítico central de una organización.

Características principales:

- Integra datos de múltiples sistemas.
- Proporciona una única versión de la verdad.
- Conserva información histórica.
- Soporta Data Marts y herramientas de BI.
- Facilita la gobernanza y la toma de decisiones.

El EDW representa el núcleo de la arquitectura analítica empresarial y sirve como base para construir soluciones escalables de Business Intelligence y Analytics.
