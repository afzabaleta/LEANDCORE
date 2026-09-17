# Equipo

## Integrantes

| Integrante | Identificación | Rol | Módulo |
|---|---|---|---|
| Andres Felipe Zabaleta Diaz | 1080574183 | Líder Técnico | Base de Datos + Arquitectura + Integración |
| Sherly Michell Corrales Maestre | 1119837499 | Desarrolladora 1 | Validaciones + Pruebas |
| Diego Armando Mestre Gomez | 1063590824 | Desarrollador 2 | Biometría + Interfaz de Usuario |

## Distribución de clases

La distribución definitiva de clases se realizará con base en el
diagrama de clases ubicado en `docs/diagrams/class-diagram.md`,
siguiendo el criterio de distribución vertical por módulo.

### Andres Felipe Zabaleta Diaz — Líder Técnico

Responsable de las clases y componentes relacionados con:

- Base de datos y persistencia.
- Gestión de préstamos.
- Motor financiero.
- Scoring crediticio.
- Integración general del sistema.

Las clases definitivas serán establecidas después de completar el
diagrama de clases del proyecto.

### Sherly Michell Corrales Maestre — Desarrolladora 1

Responsable de las clases y componentes relacionados con:

- Validaciones.
- Datos de prueba.
- Pruebas funcionales.
- Pruebas de validación.

Las clases definitivas serán establecidas después de completar el
diagrama de clases del proyecto.

### Diego Armando Mestre Gomez — Desarrollador 2

Responsable de las clases y componentes relacionados con:

- Biometría.
- Servicio biométrico simulado.
- Inicio de sesión.
- Interfaz gráfica.
- Interfaz del cliente.
- Interfaz del administrador.

Las clases definitivas serán establecidas después de completar el
diagrama de clases del proyecto.

## Actividades por integrante

### Líder Técnico — Andres Felipe Zabaleta Diaz

1. Crear el repositorio de GitHub con la configuración inicial.
2. Configurar las ramas `main` y `develop`.
3. Configurar el proyecto Maven y la estructura inicial.
4. Crear y mantener `TEAM.md`.
5. Diseñar el Modelo Entidad-Relación (MER).
6. Diseñar el modelo relacional.
7. Diseñar el diagrama de clases.
8. Diseñar el diagrama de arquitectura por capas.
9. Diseñar y administrar la base de datos Oracle.
10. Crear tablas, claves primarias, claves foráneas y restricciones.
11. Crear y organizar los scripts SQL y PL/SQL.
12. Implementar la persistencia relacionada con los préstamos.
13. Implementar el servicio de préstamos.
14. Implementar el motor de cálculos financieros.
15. Implementar el cálculo de tasas de interés.
16. Implementar el cálculo de cuotas y amortización.
17. Implementar el sistema de scoring crediticio.
18. Integrar el scoring con el proceso de solicitud de préstamo.
19. Implementar la gestión de pagos y saldos.
20. Integrar los módulos desarrollados por Sherly y Diego.
21. Revisar los Pull Requests del equipo.
22. Mantener estable la rama `develop`.
23. Realizar la integración final del proyecto.
24. Mantener actualizada la documentación principal.

### Desarrolladora 1 — Sherly Michell Corrales Maestre

1. Crear las ramas `feature` asignadas.
2. Implementar validaciones sencillas de datos del cliente.
3. Implementar validaciones básicas para formularios de préstamos.
4. Preparar datos de prueba.
5. Crear casos de prueba.
6. Ejecutar pruebas funcionales del sistema.
7. Ejecutar pruebas de validación.
8. Registrar y reportar errores encontrados.
9. Documentar los casos de prueba y sus resultados.
10. Realizar pruebas de regresión después de la integración de nuevos módulos.
11. Documentar las clases asignadas cuando corresponda.
12. Crear Pull Requests para integrar sus cambios a `develop`.

#### Restricciones durante LEANDCORE_V1

- No modificar directamente la estructura principal de Oracle.
- No modificar el motor financiero.
- No modificar el algoritmo de scoring.
- No modificar el módulo de biometría.
- No modificar la arquitectura principal sin coordinación con el Líder Técnico.
- No realizar commits directamente sobre `main` o `develop`.

### Desarrollador 2 — Diego Armando Mestre Gomez

#### Biometría

1. Crear la rama `feature/biometrics`.
2. Investigar la alternativa tecnológica de biometría.
3. Definir el servicio `BiometriaService`.
4. Implementar `MockBiometriaService` para LEANDCORE_V1.
5. Implementar escenarios básicos de verificación biométrica.
6. Probar identificación válida.
7. Probar identificación inválida.
8. Manejar errores del servicio biométrico.
9. Preparar el módulo para una futura integración con hardware real.
10. Documentar la implementación y las limitaciones de la biometría.

#### Interfaz de Usuario

11. Crear la rama `feature/login-ui`.
12. Diseñar la interfaz gráfica inicial.
13. Implementar el Login.
14. Implementar el menú principal.
15. Implementar la interfaz del cliente.
16. Implementar la interfaz del administrador.
17. Crear componentes visuales reutilizables.
18. Conectar la interfaz con las capas `Controller` y `Service`.
19. Evitar el acceso directo a la base de datos desde la interfaz.
20. Documentar las clases asignadas cuando corresponda.
21. Crear Pull Requests para integrar sus cambios a `develop`.

#### Restricciones durante LEANDCORE_V1

- No modificar directamente la estructura principal de Oracle.
- No modificar el motor financiero.
- No modificar el algoritmo de scoring.
- No modificar la arquitectura principal sin coordinación con el Líder Técnico.
- No realizar commits directamente sobre `main` o `develop`.

## Ramas del proyecto

| Integrante | Ramas principales |
|---|---|
| Líder Técnico | `feature/database`, `feature/architecture`, `feature/financial-engine`, `feature/scoring`, `feature/integration` |
| Desarrolladora 1 | `feature/validation`, `feature/testing` |
| Desarrollador 2 | `feature/biometrics`, `feature/login-ui`, `feature/client-ui`, `feature/admin-ui` |

## Flujo de trabajo con Git

Antes de comenzar una nueva funcionalidad:

```bash
git checkout develop
git pull origin develop
git checkout -b feature/nombre-de-la-funcionalidad