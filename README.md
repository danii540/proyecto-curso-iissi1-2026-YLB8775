# ACADEMIA DE FÚTBOL "Gol & Formación"

## Miembros del grupo LX-XXX-X (sustituir)

1. Urbano Castro, Ignacio
1. Lorenzo Raposo, Daniel
1. Romero Gómez, Rafael
1. Camargo Romero, Julian

## 1. Introducción al problema

La Academia de Fútbol "Gol & Formación" ha experimentado un crecimiento en su volumen de alumnos durante los últimos años. Lo que comenzó como una pequeña escuela y equipo local ha evolucionado hasta convertirse en un reconocido club deportivo. En la actualidad, la institución centra su actividad exclusivamente en la vertiente formativa y deportiva.

Gestión Deportiva y Académica: Coordinación de equipos federados y de escuela en distintas categorías de edad (desde Prebenjamín hasta Juvenil), supervisión del cuerpo técnico, planificación de   sesiones de entrenamiento en pistas específicas y control de cuotas mensuales de los alumnos. 



## 2. Glosario de términos

Los términos específicos empleados en el dominio del problema son los siguientes:

-Campo: Instalación deportiva gestionada por el Gestor en la que se desarrollan los entrenamientos o alquileres de la academia.

-Contrato: Clase de asociación que formaliza la vinculación entre un Entrenador y un Equipo, definiendo sus fechas de inicio y fin (fechaInicio, fechaFin) con una duración máxima de 1 año.

-Entrenador: Personal técnico responsable de dirigir las sesiones de entrenamiento de uno o más equipos, registrado con su nombre, teléfono y DNI.

-Equipo: Agrupación deportiva caracterizada por un grupo y una temporada, compuesta por un máximo absoluto de 25 jugadores.

-Gestor: Perfil administrativo derivado de la clase Usuario, encargado del alquiler de campos y la supervisión operativa del club.

-Jugador: Deportista derivado de la clase Usuario inscrito en la academia que participa en los entrenamientos y realiza el abono de cuotas.

-Pago: Registro transaccional que contiene el importe y la fecha abonados por el jugador, obligatorio para poder participar en las sesiones de entrenamiento.

-Participación: Clase de asociación entre Jugador y Sesión de Entrenamiento que registra la asistencia física (fechaAcude) y la evaluación deportiva (Rendimiento).

-Rendimiento: Calificación cuantitativa asignada a un jugador en una sesión de entrenamiento, acotada estrictamente en el rango de 0 a 10.

-Sesión de Entrenamiento: Bloque de tiempo acotado por fecha y hora de inicio (fechaHoraInicio) y de fin (fechaHoraFin) en el que se desarrolla la actividad deportiva de un equipo.

-Usuario: Clase base abstracta de la que heredan obligatoriamente Jugador y Gestor {completa, disjunta}, encargada de almacenar las credenciales de acceso (email y contraseña).



## 3. Visión general del sistema

### 3.1. Requisitos generales

### 3.2. Usuarios del sistema
### Tabla 1.1: Matriz de Actores, Usuarios y Perfiles del Sistema

| **Tipo de Actor** | **Rol / Perfil** | **Acceso a la Plataforma** | **Descripción y Situación Actual** | **Expectativas del Sistema** |
| :--- | :--- | :---: | :--- | :--- |
| **Gestor** | Directivo / Administración | **Sí** *(Usuario)* | Responsable de la administración global del club, gestión del personal técnico, supervisión de plantillas, control de cobros y alquiler de campos. | Disponer de un panel unificado para controlar cupos de equipos (máx. 25 jugadores), validar la duración de contratos de entrenadores (máx. 1 año) y auditar el estado de los pagos mensuales. |
| **Jugador** | Deportista / Tutor Legal | **Sí** *(Usuario)* | Alumno inscrito en la academia que participa en las sesiones de entrenamiento, realiza el abono de sus cuotas mensuales y consulta su rendimiento deportivo. | Transparencia total en el registro de sus pagos, garantía de acceso a las sesiones de entrenamiento tras estar al día en la cuota y consulta de su historial de asistencias y calificaciones (0 a 10). |
| **Entrenador** | Cuerpo Técnico | **No** *(Entidad del Dominio)* | Profesional técnico responsable de la dirección deportiva de los equipos. No interactúa directamente con el software; sus datos y contratos los gestiona el Gestor. | Mantener sus contratos vinculados formalmente a sus equipos asignados y que el Gestor pueda registrar adecuadamente la asistencia y rendimiento de sus jugadores. |

## 4. Catálogo de requisitos

### 4.1. Requisitos funcionales

#### R.F.01. Título requisito funcional

Como [tipo de usuario]
quiero [servicio]
para [razón]

**Prueba de aceptación**
- Descripción de la primera comprobación a realizar
- Descripción de la segunda comprobación a realizar
- Se debe aplicar la regla de negocio R.N.XX.
- ...

#### 4.1.1. Requisitos de información

##### R.I.01. Título requisito de información

Como [tipo de usuario]
quiero [servicio]
para [razón]

**Prueba de aceptación**
- Descripción de la primera comprobación a realizar
- Descripción de la segunda comprobación a realizar
- ...

#### 4.1.2. Reglas de negocio

##### R.N.01. Título regla negocio

Descripción de la regla de negocio.

### 4.2. Mapa de historias de usuario (opcional)

### 4.3. Requisitos no funcionales (opcional)

**R.N.F. 01. Título requisito no funcional**
Como [tipo de usuario]
quiero [servicio]
para [razón]

-- fin entregable 1 --

## 5. Modelo conceptual

### 5.1. Diagramas de clases UML

- con restricciones.

### 5.2. Escenarios de prueba

- con descripción textual y diagrama de objetos UML.

## 6. Matrices de trazabilidad

- Matriz de trazabilidad entre los elementos del modelo conceptual y los requisitos.

|       | EntidadX   | AsociaciónX  | RestricciónX  | Entidad2 ...   | 
|:------|:-----------|:-----------|:-----------|:-----------|
| RI-1  | X          | X          | X          | X          |
| RI-2  |            | X          |            | X          |
| RF-1  |            | X          |            | X          |
| RF-2  | X          |            | X          | X          |
| RN-1  |            | X          |            |            |
| RN-2  | X          | X          | X          |            |
| ...   |            |            |            |            |

-- fin entregable 2 --

## 7. Modelo relacional en 3FN

- Relaciones obtenidas al aplicar la transformación del modelo conceptual.

### 7.1.  Justificación de la estrategia de transformación de jerarquías

- si se identificaron jerarquías en el MC.


### 8. Matriz de trazabilidad MC/SQL (opcional):

- Restricciones sobre el MC / Elementos del modelo tecnológico (SQL) (Triggers, checks, etc.)
- Incluir Reglas de negocio — Constraints/Triggers en las matrices de trazabilidad para el entregable 3

|       | EntidadX   | AsociaciónX  | RestricciónX  | Entidad2 ...   | 
|:-------|:-------|:-------|:-------|:-------|
| TABLA-1 |        |        |        |        |
| TABLA-2 |        |        |        |        |
| TABLA-3 |        |        |        |        |
| TABLA-4 |        |        |        |        |
| TRIG-1 |        |        |        |        |
| TRIG-2 | X      | X      |        | X      |
| TRIG-3 |        | X      |        | X      |
| TRIG-4 |        |        | X      |        |
| CONST-1 |        |        |        |        |
| CONST-2 | X      | X      |        | X      |
| CONST-3 |        | X      |        | X      |
| CONST-4 |        |        | X      |        |

Se consideran todo tipo de constraints declarativas (aquellas definidas durante el CREATE TABLE).
-- fin entregable 3 --

## Referencias


