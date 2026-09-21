# Modelo Entidad-Relación — LEANDCORE

## 1. Propósito

Este documento define el modelo entidad-relación preliminar de LEANDCORE, estableciendo las principales entidades del sistema y las relaciones necesarias para representar el proceso de gestión de préstamos y evaluación crediticia.

El modelo será utilizado como base para la construcción posterior del modelo relacional y de la base de datos Oracle.

Las relaciones y cardinalidades indicadas en este documento corresponden a una propuesta inicial de diseño y deberán validarse durante la construcción detallada del modelo relacional y la implementación de la base de datos.

## 2. Entidades principales

Las entidades consideradas inicialmente para el sistema son:

- ROL
- PERMISO
- ROL_PERMISO
- USUARIO
- CLIENTE
- DATOS_LABORALES
- SOLICITUD_CREDITO
- SCORING
- TIPO_CREDITO
- PRESTAMO
- PLAN_AMORTIZACION
- CUOTA
- PAGO
- DESEMBOLSO
- MORA
- BIOMETRIA
- AUDITORIA
- NOTIFICACION

Estas entidades corresponden al diseño preliminar establecido para el sistema de gestión de préstamos, evaluación crediticia, seguridad, biometría, auditoría y gestión de pagos.

## 3. Relaciones y cardinalidades

Las relaciones y cardinalidades propuestas para el modelo se establecen tomando como referencia el flujo general del sistema y las entidades definidas para LEANDCORE. Estas relaciones corresponden a un diseño preliminar y deberán validarse durante la construcción detallada del modelo relacional y la base de datos Oracle.

### 3.1 ROL — USUARIO

Un rol puede estar asociado con varios usuarios, mientras que cada usuario pertenece a un rol.

**Cardinalidad propuesta:**

```text
ROL 1 ─────────── N USUARIO
```

### 3.2 ROL — PERMISO

Un rol puede tener varios permisos y un permiso puede estar asociado con varios roles. La relación se representa mediante la entidad intermedia ROL_PERMISO.

**Cardinalidad propuesta:**

```text
ROL 1 ─────────── N ROL_PERMISO N ─────────── 1 PERMISO
```

### 3.3 USUARIO — CLIENTE

Un usuario puede estar relacionado con un cliente cuando el sistema requiera asociar información de gestión o registro. Esta relación es preliminar y deberá validarse durante el diseño detallado.

**Cardinalidad propuesta:**

```text
USUARIO 1 ─────────── 0..1 CLIENTE
```

### 3.4 CLIENTE — DATOS_LABORALES

Un cliente puede registrar información laboral utilizada como parte de la información necesaria para la evaluación crediticia.

**Cardinalidad propuesta:**

```text
CLIENTE 1 ─────────── 0..1 DATOS_LABORALES
```

### 3.5 CLIENTE — SOLICITUD_CREDITO

Un cliente puede realizar varias solicitudes de crédito a lo largo del tiempo. Cada solicitud de crédito pertenece a un cliente.

**Cardinalidad propuesta:**

```text
CLIENTE 1 ─────────── N SOLICITUD_CREDITO
```

### 3.6 TIPO_CREDITO — SOLICITUD_CREDITO

Un tipo de crédito puede ser utilizado en varias solicitudes. Cada solicitud corresponde a un tipo de crédito.

**Cardinalidad propuesta:**

```text
TIPO_CREDITO 1 ─────────── N SOLICITUD_CREDITO
```

### 3.7 SOLICITUD_CREDITO — SCORING

Una solicitud de crédito puede tener asociado un resultado de evaluación de scoring.

**Cardinalidad propuesta:**

```text
SOLICITUD_CREDITO 1 ─────────── 0..1 SCORING
```

### 3.8 SCORING — PRESTAMO

Cuando una solicitud es aprobada, el resultado del scoring puede dar lugar a un préstamo.

**Cardinalidad propuesta:**

```text
SCORING 1 ─────────── 0..1 PRESTAMO
```

### 3.9 SOLICITUD_CREDITO — PRESTAMO

Una solicitud de crédito aprobada puede generar un préstamo. Una solicitud rechazada no genera necesariamente un préstamo.

**Cardinalidad propuesta:**

```text
SOLICITUD_CREDITO 1 ─────────── 0..1 PRESTAMO
```

### 3.10 PRESTAMO — PLAN_AMORTIZACION

Cada préstamo puede tener asociado un plan de amortización que contiene la estructura financiera para el pago del crédito.

**Cardinalidad propuesta:**

```text
PRESTAMO 1 ─────────── 1 PLAN_AMORTIZACION
```

### 3.11 PLAN_AMORTIZACION — CUOTA

Un plan de amortización está compuesto por varias cuotas. Cada cuota pertenece a un plan de amortización.

**Cardinalidad propuesta:**

```text
PLAN_AMORTIZACION 1 ─────────── N CUOTA
```

### 3.12 CUOTA — PAGO

Una cuota puede registrar pagos realizados por el cliente. Dependiendo de las reglas definitivas del sistema, una cuota podría admitir uno o varios registros de pago.

**Cardinalidad propuesta:**

```text
CUOTA 1 ─────────── N PAGO
```

### 3.13 PRESTAMO — DESEMBOLSO

Un préstamo aprobado puede generar un desembolso. El desembolso representa la entrega del dinero correspondiente al crédito.

**Cardinalidad propuesta:**

```text
PRESTAMO 1 ─────────── 0..1 DESEMBOLSO
```

### 3.14 CUOTA — MORA

Una cuota puede generar una mora cuando presenta incumplimiento de pago según las reglas definidas por el sistema.

**Cardinalidad propuesta:**

```text
CUOTA 1 ─────────── 0..1 MORA
```

### 3.15 USUARIO — BIOMETRIA

La información biométrica puede estar asociada a usuarios para reforzar la autenticación y proteger operaciones críticas.

**Cardinalidad propuesta:**

```text
USUARIO 1 ─────────── 0..1 BIOMETRIA
```

### 3.16 USUARIO — AUDITORIA

Las acciones relevantes realizadas por los usuarios pueden generar registros de auditoría.

**Cardinalidad propuesta:**

```text
USUARIO 1 ─────────── N AUDITORIA
```

### 3.17 CLIENTE — NOTIFICACION

Un cliente puede recibir diferentes notificaciones relacionadas con solicitudes, préstamos, cuotas, pagos u otros eventos del sistema.

**Cardinalidad propuesta:**

```text
CLIENTE 1 ─────────── N NOTIFICACION
```

### 3.18 USUARIO — NOTIFICACION

Las notificaciones también pueden estar dirigidas a usuarios internos como administradores o asesores. Esta relación es preliminar y deberá validarse durante el diseño detallado.

**Cardinalidad propuesta:**

```text
USUARIO 1 ─────────── N NOTIFICACION
```
## 4. Flujo principal representado en el modelo

El modelo entidad-relación busca representar el flujo general del sistema:

```text
CLIENTE
   │
   ▼
SOLICITUD_CREDITO
   │
   ▼
SCORING
   │
   ▼
DECISIÓN
   │
   ├──────────► RECHAZO
   │
   ▼
PRESTAMO
   │
   ├──────────► DESEMBOLSO
   │
   ▼
PLAN_AMORTIZACION
   │
   ▼
CUOTA
   │
   ├──────────► PAGO
   │
   └──────────► MORA
```

La propuesta del proyecto establece un flujo general desde el registro del cliente y la simulación, pasando por la solicitud y el scoring, hasta la decisión, desembolso, amortización, cuotas, recaudos, actualización del saldo, auditoría y reportes.

## 5. Relaciones generales del sistema

De manera resumida, las principales relaciones propuestas son:

```text
ROL
 │
 ├────────── N USUARIO
 │
 └────────── N ROL_PERMISO N ────────── PERMISO


USUARIO
 │
 ├────────── 0..1 CLIENTE
 │
 ├────────── 0..1 BIOMETRIA
 │
 ├────────── N AUDITORIA
 │
 └────────── N NOTIFICACION


CLIENTE
 │
 ├────────── 0..1 DATOS_LABORALES
 │
 ├────────── N SOLICITUD_CREDITO
 │
 └────────── N NOTIFICACION


TIPO_CREDITO
 │
 └────────── N SOLICITUD_CREDITO
                 │
                 └────────── 0..1 SCORING
                                  │
                                  └────────── 0..1 PRESTAMO
                                                   │
                              ┌────────────────────┼────────────────────┐
                              │                    │                    │
                              ▼                    ▼                    ▼
                         DESEMBOLSO       PLAN_AMORTIZACION
                                                   │
                                                   ▼
                                                 CUOTA
                                                   │
                                      ┌────────────┴────────────┐
                                      ▼                         ▼
                                    PAGO                       MORA
```

## 6. Consideraciones de diseño

- Las cardinalidades indicadas corresponden a una propuesta preliminar.
- Las relaciones deberán validarse antes de construir las tablas definitivas de Oracle.
- Las claves primarias y foráneas se definirán durante la elaboración del modelo relacional.
- Las restricciones de integridad deberán garantizar la consistencia de las relaciones entre las entidades.
- Las entidades relacionadas con seguridad, biometría y auditoría deberán diseñarse considerando los requisitos de protección de información.
- La información biométrica no deberá almacenar directamente imágenes o datos biométricos sin evaluar previamente la alternativa técnica y de seguridad correspondiente.
- Las relaciones relacionadas con pagos, mora y amortización deberán ser compatibles con las reglas del motor financiero.
- Las entidades de scoring deberán permitir conservar el resultado y los factores utilizados para la evaluación crediticia.
- Las relaciones definitivas podrán ajustarse durante la implementación de la base de datos y la integración con la aplicación Java.

## 7. Estado del modelo

**Estado:** Modelo entidad-relación preliminar.

**Siguiente etapa:** convertir este modelo en el modelo relacional, definiendo:

- Claves primarias.
- Claves foráneas.
- Atributos de cada entidad.
- Tipos de datos.
- Restricciones de integridad.
- Índices necesarios.
- Secuencias de Oracle.
- Relaciones definitivas.
- Normalización del modelo.

El modelo relacional será posteriormente utilizado como base para la implementación de las tablas y demás objetos de la base de datos Oracle.
