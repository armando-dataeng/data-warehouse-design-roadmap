# BUSINESS KEYS

## Definición

Una Business Key es un identificador proveniente del sistema fuente que representa de forma única una entidad dentro del negocio.

Tiene significado para los usuarios y para las aplicaciones operacionales.

Ejemplos:

```text
CustomerID

ProductCode

InvoiceNumber

EmployeeNumber
```

---

# ¿Por qué existen?

Las aplicaciones necesitan identificar entidades del negocio.

Ejemplo:

Sistema CRM:

```text
CustomerID = CUST100
```

---

Sistema ERP:

```text
ProductCode = PRD-001
```

---

Sistema Bancario:

```text
AccountNumber = ACC-987654
```

---

Todos son:

```text
Business Keys.
```

---

# Características

Una Business Key:

- Proviene del sistema fuente.
- Tiene significado para el negocio.
- Puede ser utilizada por usuarios.
- Puede cambiar con el tiempo.
- Debe mantenerse para trazabilidad.

---

# Ejemplo

Sistema Operacional:

| CustomerID | CustomerName |
|------------|--------------|
| CUST100 | Pedro |

---

Data Warehouse:

| CustomerKey | CustomerID | CustomerName |
|------------|------------|--------------|
| 10 | CUST100 | Pedro |

---

Observación:

```text
CustomerKey
```

es la:

```text
Surrogate Key
```

---

Mientras que:

```text
CustomerID
```

es la:

```text
Business Key
```

---

# ¿Por qué conservar la Business Key?

Aunque el Data Warehouse utilice Surrogate Keys para las relaciones, la Business Key sigue siendo necesaria para:

- Identificar registros provenientes del sistema fuente.
- Integrar datos entre sistemas.
- Detectar nuevos registros.
- Implementar procesos ETL/ELT.
- Facilitar auditorías.

---

# Ejemplo de ETL

Sistema Fuente:

| CustomerID | CustomerName |
|------------|--------------|
| CUST100 | Pedro |

---

Durante la carga:

```text
Buscar:

CustomerID = CUST100
```

---

Si existe:

```text
Actualizar dimensión.
```

---

Si no existe:

```text
Crear nuevo registro.
```

---

La búsqueda se realiza utilizando:

```text
Business Key.
```

---

# Relación con SCD Type 2

Antes:

| CustomerKey | CustomerID | City |
|------------|------------|------|
| 10 | CUST100 | Miami |

---

Cambio:

```text
Orlando
```

---

Después:

| CustomerKey | CustomerID | City |
|------------|------------|------|
| 10 | CUST100 | Miami |
| 11 | CUST100 | Orlando |

---

Observación:

```text
Business Key
```

permanece igual.

---

Mientras que cambia:

```text
Surrogate Key.
```

---

Esto permite:

```text
Conservar historial.
```

---

# Business Key vs Surrogate Key

| Característica | Business Key | Surrogate Key |
|---------------|--------------|---------------|
| Origen | Sistema fuente | Data Warehouse |
| Significado | Sí | No |
| Puede cambiar | Sí | No |
| Visible para usuarios | Sí | No |
| Utilizada en relaciones | Generalmente no | Sí |

---

# Caso Real

Empresa:

```text
CRM

ERP

E-commerce
```

---

Cada sistema utiliza:

```text
CustomerID
```

---

Durante la integración:

```text
CustomerID
```

permite identificar al mismo cliente.

---

El Data Warehouse genera:

```text
CustomerKey
```

para manejar las relaciones internas.

---

# Ejemplo Completo

## DimCustomer

| CustomerKey | CustomerID | CustomerName | City |
|------------|------------|--------------|------|
| 10 | CUST100 | Pedro | Miami |

---

## FactSales

| CustomerKey | SalesAmount |
|------------|-------------|
| 10 | 1500 |

---

Consulta para auditoría:

```text
Buscar cliente CUST100.
```

---

Se utiliza:

```text
Business Key.
```

---

# Beneficios

## Integración

Permite relacionar múltiples sistemas.

---

## Trazabilidad

Conecta el Data Warehouse con el origen.

---

## Auditoría

Facilita validar datos.

---

## Procesos ETL

Permite identificar registros existentes.

---

## Compatibilidad

Los usuarios reconocen estos identificadores.

---

# Buenas prácticas

## Conservar siempre la Business Key

Nunca eliminarla.

---

## Utilizar Surrogate Keys para relaciones

No utilizar Business Keys como Foreign Keys.

---

## Validar unicidad

La Business Key debe identificar una entidad en su sistema de origen.

---

## Documentar su origen

Indicar de qué sistema proviene.

---

## Mantener sincronización

Con los sistemas operacionales.

---

# Error común

Muchos principiantes utilizan:

```text
CustomerID
```

como Primary Key de la dimensión.

---

Problemas:

- Cambios en el sistema fuente.
- Integración compleja.
- Dificultades con SCD Type 2.

---

# Error conceptual frecuente

Muchos creen:

```text
Business Key
=
Primary Key
```

---

Incorrecto.

En un Data Warehouse normalmente:

```text
Primary Key

↓

Surrogate Key
```

---

Mientras que:

```text
Business Key
```

se conserva como un atributo.

---

# Caso de Entrevista

Pregunta:

```text
¿Por qué mantener
la Business Key
si ya existe una Surrogate Key?
```

---

Respuesta:

```text
Porque la Business Key permite
identificar registros provenientes
de los sistemas fuente,
facilita procesos ETL,
integración, auditoría
y trazabilidad,
mientras que la Surrogate Key
se utiliza para las relaciones
internas del Data Warehouse.
```

---

# Pensamiento de Data Warehouse

Antes de diseñar una dimensión pregúntate:

1. ¿Cuál es la Business Key del sistema fuente?
2. ¿Es única dentro de ese sistema?
3. ¿Puede cambiar con el tiempo?
4. ¿Cómo la utilizaré durante el ETL?
5. ¿Cómo la relacionaré con la Surrogate Key?
6. ¿Necesito conservarla para auditoría?
7. ¿Qué ocurrirá si cambia en el sistema origen?

---

# Relación con los siguientes módulos

```text
SURROGATE KEYS
        ↓
BUSINESS KEYS
        ↓
DATE DIMENSION
        ↓
JUNK DIMENSIONS
        ↓
BRIDGE TABLES
```

---

# Resumen

Las Business Keys son identificadores de negocio provenientes de los sistemas fuente.

Características principales:

- Tienen significado para el negocio.
- Se utilizan para integración y trazabilidad.
- Son fundamentales en procesos ETL/ELT.
- Pueden cambiar con el tiempo.

En un Data Warehouse moderno:

- Las **Surrogate Keys** se utilizan para relacionar tablas.
- Las **Business Keys** se conservan para mantener la conexión con los sistemas de origen y facilitar la gestión del ciclo de vida de los datos.
