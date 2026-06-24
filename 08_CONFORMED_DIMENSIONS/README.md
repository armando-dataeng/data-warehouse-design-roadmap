# CONFORMED DIMENSIONS

## Definición

Una Conformed Dimension es una dimensión compartida que mantiene la misma estructura, significado y valores en múltiples Fact Tables o Data Marts.

Su objetivo es garantizar que todas las áreas de la organización utilicen una única versión consistente de la información.

---

# ¿Por qué existen?

Imaginemos una empresa con varios departamentos:

```text
Ventas

Compras

Inventario

Finanzas
```

---

Todos utilizan información de clientes.

---

Pregunta:

```text
¿Cada departamento
debería tener
su propia DimCustomer?
```

---

Respuesta:

```text
No.
```

---

Todos deberían utilizar:

```text
La misma DimCustomer.
```

---

# Problema Sin Conformed Dimensions

Ventas:

```text
DimCustomer
```

---

Marketing:

```text
CustomerDimension
```

---

Finanzas:

```text
Clientes
```

---

Cada una tiene:

- Diferentes columnas
- Diferentes claves
- Diferentes definiciones

---

Resultado:

```text
Métricas inconsistentes.
```

---

# Solución

Compartir una única dimensión.

---

Arquitectura:

```text
             DimCustomer
             /    |    \
            /     |     \
           /      |      \
FactSales FactOrders FactSupport
```

---

Todos utilizan:

```text
La misma dimensión.
```

---

# Características

Una Conformed Dimension debe:

- Tener la misma estructura.
- Utilizar las mismas claves.
- Mantener el mismo significado.
- Ser compartida por múltiples procesos.

---

# Ejemplo

## DimCustomer

| CustomerKey | CustomerName | City | Country |
|------------|--------------|------|---------|
| 10 | Pedro | Miami | USA |

---

FactSales

| CustomerKey | SalesAmount |
|------------|-------------|
| 10 | 1500 |

---

FactOrders

| CustomerKey | Orders |
|------------|--------|
| 10 | 5 |

---

FactSupport

| CustomerKey | Tickets |
|------------|---------|
| 10 | 3 |

---

Todas las tablas utilizan:

```text
CustomerKey
```

---

# Beneficios

## Consistencia

Todos utilizan la misma definición.

---

## Reutilización

Una dimensión sirve para múltiples procesos.

---

## Integración

Facilita combinar información.

---

## Menor mantenimiento

Los cambios se realizan una sola vez.

---

# Caso Real

## Empresa Retail

Fact Tables:

```text
FactSales

FactReturns

FactInventory

FactShipments
```

---

Todas utilizan:

```text
DimProduct

DimCustomer

DimDate

DimStore
```

---

Pregunta:

```text
¿Cuáles son los productos
más vendidos
y con más devoluciones?
```

---

Respuesta:

Se pueden combinar fácilmente porque ambas tablas utilizan la misma:

```text
DimProduct
```

---

# Integración Entre Data Marts

Sin Conformed Dimensions:

```text
Sales Mart

Marketing Mart

Finance Mart
```

---

Cada uno tiene:

```text
DimCustomer diferente
```

---

Integración:

```text
Muy difícil.
```

---

Con Conformed Dimensions:

```text
Sales Mart
      \
       \
        DimCustomer
       /
      /
Finance Mart
```

---

Resultado:

```text
Integración sencilla.
```

---

# Dimensiones Comúnmente Compartidas

## DimCustomer

Clientes.

---

## DimProduct

Productos.

---

## DimDate

Fechas.

---

## DimStore

Tiendas.

---

## DimEmployee

Empleados.

---

# Ejemplo Analítico

Pregunta:

```text
Ventas
vs
Devoluciones
por Cliente.
```

---

Consulta conceptual:

```text
FactSales
      ↓

DimCustomer

      ↑

FactReturns
```

---

Ambas utilizan:

```text
La misma dimensión.
```

---

# Reglas

Una Conformed Dimension debe:

## Mantener los mismos atributos

---

Ejemplo:

```text
CustomerName

City

Country
```

---

No cambiar entre procesos.

---

## Mantener las mismas claves

Ejemplo:

```text
CustomerKey = 10
```

---

Debe representar siempre:

```text
Pedro
```

---

## Mantener la misma semántica

La definición de:

```text
Cliente Activo
```

debe ser igual para toda la organización.

---

# Ventajas

## Reporting consistente

---

## KPIs confiables

---

## Integración empresarial

---

## Reutilización

---

## Gobernanza de datos

---

# Desafíos

## Administración

Una dimensión compartida requiere mayor control.

---

## Cambios

Modificar una dimensión puede afectar múltiples procesos.

---

## Gobierno

Es necesario definir propietarios y reglas claras.

---

# Buenas prácticas

## Compartir dimensiones comunes

Cliente, Producto, Fecha.

---

## Mantener claves estables

Evitar cambios innecesarios.

---

## Documentar atributos

Facilitar mantenimiento.

---

## Aplicar estándares

Nombres consistentes.

---

## Controlar cambios

Especialmente cuando existen múltiples consumidores.

---

# Error común

Muchos equipos crean:

```text
Una DimCustomer
para cada Data Mart.
```

---

Resultado:

```text
Datos inconsistentes.

KPIs diferentes.

Duplicación.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Conformed Dimension
=
Tabla compartida físicamente.
```

---

Incorrecto.

Lo importante es:

```text
Compartir
estructura,
claves
y significado.
```

---

Puede existir una única tabla física o copias sincronizadas, siempre que mantengan la misma definición.

---

# Caso de Entrevista

Pregunta:

```text
¿Qué es una Conformed Dimension?
```

---

Respuesta:

```text
Es una dimensión compartida entre múltiples Fact Tables o Data Marts que mantiene la misma estructura, claves y significado para garantizar consistencia e integración en todo el Data Warehouse.
```

---

# Pensamiento de Data Warehouse

Antes de crear una dimensión pregúntate:

1. ¿Será utilizada por más de un proceso?
2. ¿Puede reutilizarse en otros Data Marts?
3. ¿Sus atributos son consistentes?
4. ¿Las claves permanecerán estables?
5. ¿Qué impacto tendrán los cambios?
6. ¿Existe una única definición del negocio?
7. ¿Facilitará la integración entre áreas?

---

# Relación con los siguientes módulos

```text
DIMENSION TABLES
        ↓
CONFORMED DIMENSIONS
        ↓
DEGENERATE DIMENSIONS
        ↓
FACTLESS FACT TABLES
        ↓
SCD TYPES
```

---

# Resumen

Las Conformed Dimensions son dimensiones compartidas que garantizan consistencia entre múltiples procesos analíticos.

Conceptos principales:

- Dimensiones compartidas
- Consistencia empresarial
- Integración entre Data Marts
- Reutilización
- Gobernanza

Son uno de los pilares de la metodología de Ralph Kimball y permiten construir Data Warehouses escalables, consistentes y fáciles de mantener.
