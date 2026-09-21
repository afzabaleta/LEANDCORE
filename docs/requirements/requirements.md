# Requerimientos del sistema — LEANDCORE

## 1. Descripción del sistema

LEANDCORE es un sistema de gestión de préstamos orientado a administrar el ciclo de crédito desde la simulación y solicitud hasta la aprobación, desembolso, generación de cuotas y recaudo.

El sistema incorpora componentes de seguridad, evaluación crediticia, cálculos financieros, auditoría y autenticación biométrica, utilizando una arquitectura modular y una base de datos relacional.

El proyecto está orientado al desarrollo académico en Java, utilizando una arquitectura por capas, patrón DAO, Oracle Database y PL/SQL.

## 2. Objetivo general

Diseñar e implementar LEANDCORE, un sistema de gestión de préstamos desarrollado en Java con arquitectura en capas y patrón DAO, respaldado por una base de datos relacional en Oracle, capaz de administrar clientes, solicitudes, evaluación crediticia, préstamos, amortizaciones, desembolsos, recaudos y reportes, incorporando mecanismos de seguridad, auditoría y autenticación biométrica.

## 3. Objetivos específicos

- Implementar la gestión de usuarios, roles y permisos.
- Gestionar la información de los clientes.
- Desarrollar un módulo para simular préstamos.
- Generar tablas de amortización.
- Implementar conversiones entre tasas de interés.
- Realizar cálculos financieros relacionados con préstamos.
- Implementar un proceso de solicitud y evaluación de crédito mediante un scoring basado en reglas.
- Gestionar la aprobación y rechazo de solicitudes de crédito.
- Gestionar el desembolso de préstamos.
- Registrar cuotas, pagos, abonos extraordinarios, mora y saldos pendientes.
- Implementar mecanismos de autenticación y autorización.
- Incorporar un mecanismo biométrico viable y desacoplado.
- Implementar un módulo de auditoría para registrar operaciones importantes.
- Desarrollar reportes e indicadores del sistema.
- Utilizar Oracle y PL/SQL mediante procedimientos, funciones, triggers, vistas, secuencias y restricciones.
- Mantener una arquitectura modular que permita ampliar el sistema posteriormente.

## 4. Alcance

El proyecto se divide en un núcleo funcional obligatorio y componentes diferenciadores.

### 4.1 Núcleo funcional

El núcleo del sistema contempla:

- Usuarios y roles.
- Clientes.
- Solicitudes de crédito.
- Scoring crediticio.
- Préstamos.
- Amortización.
- Pagos y recaudos.
- Oracle Database y PL/SQL.
- Reportes.
- Auditoría.

### 4.2 Componentes diferenciadores

Como componentes diferenciadores del proyecto se contemplan:

- Biometría.
- Dashboard avanzado.
- Asistente inteligente.
- Simulación de abonos extraordinarios.

Los componentes diferenciadores se desarrollarán de acuerdo con la disponibilidad de tiempo, recursos y viabilidad técnica del proyecto.

## 5. Actores del sistema

### 5.1 Administrador

Actor encargado de administrar usuarios, roles, permisos y operaciones administrativas del sistema.

### 5.2 Asesor / Cajero

Actor encargado de participar en la gestión de solicitudes, préstamos, desembolsos y recaudos de acuerdo con los permisos asignados.

### 5.3 Cliente

Actor que puede registrar y consultar información relacionada con sus solicitudes, préstamos, cuotas y obligaciones.

## 6. Requerimientos funcionales

### RF-01. Gestión de usuarios

El sistema debe permitir registrar, actualizar y consultar usuarios.

### RF-02. Gestión de roles y permisos

El sistema debe permitir administrar roles y controlar los permisos asociados a cada rol.

### RF-03. Inicio de sesión

El sistema debe permitir la autenticación de los usuarios mediante credenciales.

### RF-04. Gestión de clientes

El sistema debe permitir registrar y actualizar la información personal y laboral de los clientes.

### RF-05. Consulta del historial del cliente

El sistema debe permitir consultar el historial de solicitudes y créditos asociados a un cliente.

### RF-06. Simulación de crédito

El sistema debe permitir simular un préstamo utilizando como mínimo:

- Monto solicitado.
- Plazo.
- Tipo de tasa.
- Tasa de interés.
- Frecuencia de pago.

### RF-07. Cálculo de cuotas

El sistema debe calcular el valor de las cuotas correspondientes a una simulación o préstamo.

### RF-08. Generación de tabla de amortización

El sistema debe generar una tabla de amortización mostrando la distribución de capital, intereses y saldo.

### RF-09. Registro de solicitud

El sistema debe permitir registrar formalmente una solicitud de crédito.

### RF-10. Evaluación crediticia

El sistema debe evaluar las solicitudes mediante un sistema de scoring basado en reglas.

### RF-11. Resultado del scoring

El sistema debe generar un resultado de evaluación que pueda clasificarse como:

- Aprobado.
- Condicionado.
- Rechazado.

### RF-12. Explicación del scoring

El sistema debe registrar los factores que influyeron en el resultado de la evaluación crediticia.

### RF-13. Gestión de préstamos

El sistema debe permitir gestionar los préstamos aprobados y su información financiera.

### RF-14. Aprobación o rechazo

El sistema debe permitir registrar la decisión correspondiente sobre una solicitud de crédito.

### RF-15. Desembolso

El sistema debe permitir registrar el desembolso asociado a un préstamo aprobado.

### RF-16. Gestión de cuotas

El sistema debe permitir registrar y consultar las cuotas correspondientes a cada préstamo.

### RF-17. Registro de pagos

El sistema debe permitir registrar los pagos realizados sobre las cuotas.

### RF-18. Abonos extraordinarios

El sistema debe permitir gestionar abonos extraordinarios cuando esta funcionalidad se encuentre habilitada.

### RF-19. Actualización de saldos

El sistema debe actualizar el saldo pendiente del préstamo después de las operaciones financieras correspondientes.

### RF-20. Gestión de mora

El sistema debe permitir registrar y controlar la mora de acuerdo con las reglas financieras definidas para el proyecto.

### RF-21. Historial de pagos

El sistema debe permitir consultar el historial de pagos realizados.

### RF-22. Auditoría

El sistema debe registrar las operaciones importantes realizadas en el sistema.

La auditoría debe contemplar como mínimo:

- Usuario que ejecutó la acción.
- Operación realizada.
- Fecha y hora.
- Módulo afectado.
- Resultado de la operación.

### RF-23. Seguridad y biometría

El sistema debe contemplar mecanismos de validación biométrica para operaciones críticas, de acuerdo con la implementación disponible.

### RF-24. Reportes

El sistema debe permitir generar información relacionada con:

- Créditos activos.
- Créditos vencidos.
- Cartera.
- Recaudos.
- Solicitudes pendientes.
- Indicadores financieros.

### RF-25. Dashboard

El sistema podrá incorporar un dashboard para visualizar indicadores y gráficas relacionadas con la operación del sistema.

### RF-26. Asistente inteligente

Como componente diferenciador, el sistema podrá incorporar un asistente para realizar consultas controladas relacionadas con:

- Saldo pendiente.
- Pagos realizados.
- Próxima cuota.
- Simulación de escenarios.
- Abonos extraordinarios.
- Número de cuotas pendientes.

## 7. Requerimientos no funcionales

### RNF-01. Arquitectura

El sistema debe utilizar una arquitectura por capas que permita separar la interfaz, los controladores, los servicios, la persistencia y el modelo.

### RNF-02. Persistencia

La información del sistema debe almacenarse en una base de datos relacional Oracle.

### RNF-03. Acceso a datos

El acceso a la base de datos debe realizarse mediante una capa de persistencia basada en el patrón DAO.

### RNF-04. Integridad de datos

La base de datos debe utilizar claves primarias, claves foráneas y restricciones de integridad como NOT NULL, UNIQUE y CHECK cuando correspondan.

### RNF-05. Seguridad

Las contraseñas no deben almacenarse en texto plano y el acceso a las funcionalidades debe estar controlado mediante roles y permisos.

### RNF-06. Protección de información sensible

El sistema debe evitar exponer credenciales y otra información sensible mediante la aplicación o los mensajes de error.

### RNF-07. Transacciones

Las operaciones financieras deben utilizar transacciones que permitan mantener la consistencia de los datos.

### RNF-08. Auditoría

Las operaciones críticas deben generar registros de auditoría.

### RNF-09. Modularidad

El sistema debe mantener una estructura modular que facilite la incorporación de nuevas funcionalidades.

### RNF-10. Mantenibilidad

La separación de responsabilidades debe facilitar el mantenimiento, las pruebas y la evolución del sistema.

### RNF-11. Validación

Los datos ingresados por los usuarios deben ser validados antes de ser procesados.

### RNF-12. Manejo de excepciones

El sistema debe manejar las excepciones de forma controlada sin exponer información sensible.

## 8. Reglas de negocio preliminares

### RN-01. Roles

Cada usuario debe estar asociado a un rol que determine las funcionalidades a las que puede acceder.

### RN-02. Solicitud de crédito

Una solicitud debe contener la información necesaria para realizar su evaluación y posterior decisión.

### RN-03. Evaluación crediticia

La evaluación crediticia debe considerar reglas y factores definidos para el scoring.

### RN-04. Resultado de evaluación

El scoring debe producir un resultado explicable y registrar los factores que influyeron en la evaluación.

### RN-05. Préstamo

Un préstamo debe estar asociado a un cliente y contar con las condiciones financieras correspondientes.

### RN-06. Cuotas

Cada préstamo debe contar con un plan de pagos y sus respectivas cuotas.

### RN-07. Pagos

Los pagos deben estar asociados a las cuotas correspondientes y actualizar los valores financieros relacionados.

### RN-08. Auditoría

Las operaciones críticas deben conservar información sobre el usuario que realizó la operación y el momento en que fue ejecutada.

### RN-09. Biometría

La validación biométrica debe mantenerse desacoplada del resto del sistema para permitir el uso de diferentes proveedores o mecanismos compatibles.

### RN-10. Información biométrica

La implementación biométrica debe evitar almacenar directamente imágenes o datos biométricos cuando la tecnología seleccionada permita utilizar identificadores o plantillas.

## 9. Flujo general del sistema

El flujo general propuesto para el sistema es:

```text
1. Registro del cliente
        ↓
2. Inicio de sesión y validación de identidad
        ↓
3. Simulación del préstamo
        ↓
4. Creación de la solicitud
        ↓
5. Evaluación mediante scoring
        ↓
6. Revisión y decisión
        ↓
7. Validación biométrica de la operación crítica
        ↓
8. Desembolso
        ↓
9. Generación del plan de amortización
        ↓
10. Registro de cuotas y recaudos
        ↓
11. Actualización del saldo y estado
        ↓
12. Reportes y auditoría