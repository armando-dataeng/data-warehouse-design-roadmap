# INMON METHODOLOGY

## Definición

La Metodología Inmon es un enfoque para diseñar e implementar Data Warehouses basado en la construcción de un Enterprise Data Warehouse (EDW) centralizado y normalizado antes de crear Data Marts.

Fue propuesta por Bill Inmon y se caracteriza por seguir una estrategia Top-Down.

Su objetivo es construir una plataforma de datos empresarial integrada que sirva como fuente única de verdad para toda la organización.

---

# ¿Quién es Bill Inmon?

Bill Inmon es considerado:

```text
El Padre del Data Warehouse.
```

---

Fue uno de los primeros en definir formalmente el concepto de:

```text
Enterprise Data Warehouse
```

---

Su definición clásica establece que un Data Warehouse es:

```text
Orientado a temas

Integrado

No volátil

Variable en el tiempo
```

---

Estos cuatro principios siguen siendo la base de muchos Data Warehouses modernos.

---

# Filosofía

Inmon propone:

```text
Construir primero

↓

Enterprise Data Warehouse

↓

Después

↓

Data Marts
```

---

Este enfoque se conoce como:

```text
Top-Down.
```

---

# Arquitectura

```text
Operational Systems

        ↓

ETL / ELT

        ↓

Enterprise Data Warehouse
(Normalizado)

        ↓

Data Marts

        ↓

Power BI
Tableau
Looker
```

---

El EDW se convierte en la fuente oficial de datos.

---

# Principios Fundamentales

## Enterprise First

El diseño comienza pensando en:

```text
Toda la organización.
```

---

No en un único departamento.

---

## Modelo Normalizado

El Enterprise Data Warehouse suele diseñarse utilizando:

```text
Tercera Forma Normal (3NF)
```

---

Objetivos:

```text
Reducir redundancia.

Mantener consistencia.

Facilitar mantenimiento.
```

---

## Data Marts Derivados

Los Data Marts se construyen posteriormente.

---

Arquitectura:

```text
EDW

↓

Sales Mart

Finance Mart

Marketing Mart
```

---

Todos provienen del mismo origen.

---

# Ciclo de Diseño

## Paso 1

Identificar dominios empresariales.

---

Ejemplo:

```text
Clientes

Productos

Ventas

Finanzas

Recursos Humanos
```

---

## Paso 2

Diseñar un modelo corporativo normalizado.

---

## Paso 3

Integrar todas las fuentes de datos.

---

## Paso 4

Construir el Enterprise Data Warehouse.

---

## Paso 5

Generar Data Marts específicos.

---

# Arquitectura Empresarial

```text
CRM

ERP

POS

HR

Finance

       ↓

ETL / ELT

       ↓

Enterprise Data Warehouse

       ↓

Sales Mart

Finance Mart

Marketing Mart

Operations Mart
```

---

El EDW es la única fuente para todos los Data Marts.

---

# Ventajas

## Alta consistencia

Existe una única versión de la verdad.

---

## Excelente integración

Todos los datos pasan por el EDW.

---

## Menor duplicación

La normalización reduce redundancia.

---

## Escalabilidad

Adecuado para organizaciones grandes.

---

## Gobierno de datos

Facilita estándares y calidad.

---

# Desventajas

## Mayor tiempo inicial

El EDW debe construirse antes de entregar resultados.

---

## Mayor complejidad

Diseñar un modelo corporativo requiere más esfuerzo.

---

## Menor velocidad de entrega

Los usuarios esperan más tiempo para obtener valor.

---

# Caso Real

Empresa Multinacional.

Fuentes:

```text
SAP

Salesforce

Oracle

Workday

Shopify
```

---

Todas las fuentes se integran primero en:

```text
Enterprise Data Warehouse
```

---

Después se crean:

```text
Sales Mart

Finance Mart

HR Mart
```

---

Cada Data Mart reutiliza los datos del EDW.

---

# Inmon vs Kimball

| Característica | Inmon | Kimball |
|---------------|--------|----------|
| Estrategia | Top-Down | Bottom-Up |
| Punto de partida | Enterprise Data Warehouse | Data Marts |
| Modelo principal | Normalizado (3NF) | Dimensional |
| Entrega inicial | Más lenta | Más rápida |
| Integración | Desde el inicio | Progresiva |
| Complejidad inicial | Alta | Moderada |

---

# ¿Cuándo utilizar Inmon?

Es recomendable cuando:

- La organización es muy grande.
- Existen múltiples sistemas empresariales.
- La gobernanza es una prioridad.
- Se busca una arquitectura corporativa de largo plazo.
- La integración entre áreas es crítica.

---

# ¿Cuándo utilizar Kimball?

Es recomendable cuando:

- Se necesitan resultados rápidos.
- Se desarrollan soluciones de BI incrementales.
- Se trabaja con metodologías ágiles.
- El enfoque está orientado a análisis y reporting.

---

# Buenas prácticas

## Diseñar un modelo empresarial

Antes de crear Data Marts.

---

## Integrar todas las fuentes

Mantener una visión unificada.

---

## Normalizar el EDW

Reducir redundancia.

---

## Construir Data Marts desde el EDW

Evitar conexiones directas con sistemas operacionales.

---

## Definir estándares corporativos

Para datos, métricas y nomenclatura.

---

# Error común

Muchos equipos crean:

```text
Data Marts

↓

Directamente

↓

Desde sistemas fuente.
```

---

Resultado:

```text
Duplicación.

Inconsistencias.

Múltiples versiones
de la verdad.
```

---

La metodología Inmon propone:

```text
Enterprise Data Warehouse

↓

Data Marts.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Inmon

=

No utiliza
Star Schema.
```

---

Incorrecto.

El EDW suele estar normalizado.

Pero los Data Marts derivados pueden utilizar:

```text
Star Schema

Snowflake Schema

Modelado Dimensional
```

---

# Caso de Entrevista

Pregunta:

```text
¿Qué propone
la metodología Inmon?
```

---

Respuesta:

```text
Inmon propone construir primero un Enterprise Data Warehouse integrado y normalizado utilizando un enfoque Top-Down. Posteriormente, los Data Marts se generan a partir del EDW para satisfacer las necesidades analíticas de cada área del negocio.
```

---

# Kimball vs Inmon

```text
Kimball

↓

Data Marts

↓

Enterprise Data Warehouse
```

---

```text
Inmon

↓

Enterprise Data Warehouse

↓

Data Marts
```

---

Ambas metodologías buscan:

```text
Una única versión
de la verdad.
```

---

La diferencia está en:

```text
El orden
de construcción.
```

---

# Pensamiento de Arquitectura

Antes de elegir una metodología pregúntate:

1. ¿Qué tan grande es la organización?
2. ¿Qué tan importante es la gobernanza?
3. ¿Necesito resultados rápidos?
4. ¿Cuántos sistemas debo integrar?
5. ¿Qué recursos tiene el equipo?
6. ¿Cuál es la estrategia tecnológica de largo plazo?
7. ¿Cómo evolucionará la plataforma de datos?

---

# Relación con los siguientes módulos

```text
KIMBALL METHODOLOGY
        ↓
INMON METHODOLOGY
        ↓
DATA WAREHOUSE CASE STUDY
```

---

# Resumen

La Metodología Inmon es un enfoque Top-Down para construir Data Warehouses.

Principios principales:

- Enterprise Data Warehouse primero.
- Modelo corporativo normalizado (3NF).
- Data Marts derivados del EDW.
- Alta integración.
- Fuerte enfoque en gobernanza.

Comparación:

```text
Kimball

↓

Bottom-Up

↓

Data Marts primero

↓

Modelado Dimensional
```

```text
Inmon

↓

Top-Down

↓

Enterprise Data Warehouse primero

↓

Modelo Normalizado
```

Ambas metodologías son referentes del Data Warehousing moderno y continúan influyendo en el diseño de plataformas analíticas. Muchas organizaciones actuales combinan principios de ambas para aprovechar la rapidez de Kimball y la solidez arquitectónica de Inmon.
