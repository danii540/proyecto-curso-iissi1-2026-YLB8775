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


El sistema de gestión de la academia de fútbol se basa en la gestión administrativa y el control de instalaciones. Los requisitos generales que definen el alcance del sistema son los siguientes:

* **Gestión Unificada de Usuarios y Autenticación:** Implementación de una arquitectura de usuarios jerárquica `{completa, disjunta}` basada en la entidad base **Usuario** (credenciales de `email` y `contraseña`), especializándose de manera obligatoria y exclusiva en los perfiles **Jugador** y **Gestor**.

* **Control Financiero y Condicionamiento de Acceso (R01):** Verificación del cumplimiento del abono mensual (**Pago:** `importe`, `fecha`) por parte del **Jugador** como requisito indispensable para quedar habilitado y participar en las sesiones de entrenamiento.

* **Gestión de Plantillas y Control de Cupos (R02):** Administración de los equipos (**Equipo:** `grupo`, `temporada`) y supervisión estricta de la relación con los jugadores, garantizando que un equipo no supere el límite máximo de 25 jugadores.
  
* **Gestión Contractual del Cuerpo Técnico (R03):** Registro y control de la vinculación entre entrenadores y equipos mediante la entidad intermedia **Contrato** (`fechaInicio`, `fechaFin`), limitando la duración máxima de cada contrato a 1 año.
  
* **Planificación y Evaluación Deportiva (R03):** Programación de sesiones de entrenamiento (**SesionEntrenamiento:** `fechaHoraInicio`, `fechaHoraFin`) y registro individualizado del rendimiento del jugador a través de la clase de asociación **Partición** (`fechaAcude`, `Rendimiento`), asegurando que las calificaciones se mantengan estrictamente en el rango numérico de 0 a 10.
  
* **Administración de Instalaciones:** Gestión del catálogo de campos deportivos (**Campo**) por parte del perfil **Gestor**, permitiendo su control y reserva operativa.




### 3.2. Usuarios del sistema

Nuestro sistema clasifica a los usuarios que interactúan directamente con la plataforma mediante una jerarquía de herencia completa y disjunta derivada de la clase base abstracta Usuario.

La entidad base Usuario es la encargada de almacenar las credenciales de acceso al sistema (email y contraseña). De esta clase abstracta se derivan de forma obligatoria y exclusiva {completa, disjunta} los dos únicos perfiles con acceso a la plataforma: el Jugador y el Gestor. Esta arquitectura garantiza que todo usuario en el sistema pertenezca estrictamente a uno de estos dos tipos.

| **Tipo de Actor** | **Rol / Perfil** | **Descripción y Situación Actual** | **Expectativas del Nuevo Sistema** |
| :--- | :--- | :--- | :--- |
| **Usuario** | Jugador | Alumno inscrito en la escuela formativa que pertenece a una categoría concreta y realiza el abono periódico de las cuotas mensuales. | Transparencia total en el estado de sus pagos/cuotas, asignación garantizada de sus horarios y campos de entrenamiento, y correcta categorización por edad. |
| **Gestor** | Directivo de la academia | Encargado de la gestión global de la academia, del alquiler de los campos donde se realizan las sesiones de entrenamiento. | Disponer de un panel centralizado para gestionar altas de jugadores, automatizar el control de cobros e impagos, asignar pistas sin solapamientos y supervisar los cupos por equipo.. |

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


