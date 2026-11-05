# ACADEMIA DE FÚTBOL "Gol & Formación"
 
## Miembros del grupo L6-DF-8 

1. Urbano Castro, Ignacio
2. Lorenzo Raposo, Daniel
3. Romero Gómez, Rafael
4. Camargo Moral, Julian

## 1. Introducción al problema

La Academia de Fútbol "Gol & Formación" ha experimentado un crecimiento en su volumen de alumnos durante los últimos años. Lo que comenzó como una pequeña escuela y equipo local ha evolucionado hasta convertirse en un reconocido club deportivo. En la actualidad, la institución centra su actividad exclusivamente en la vertiente formativa y deportiva.

Gestión Deportiva y Académica: Coordinación de equipos federados y de escuela en distintas categorías de edad (desde Prebenjamín hasta Juvenil), supervisión del cuerpo técnico, planificación de   sesiones de entrenamiento en pistas específicas y control de cuotas mensuales de los alumnos. 



## 2. Glosario de términos

Los términos específicos empleados en el dominio del problema son los siguientes:

* **Campo:** Instalación deportiva que el Gestor alquila para la realización de entrenamientos. El modelo conceptual solo recoge sus atributos ubicación y estado, su estado puede ser activo o inactivo.

* **Equipo:** Grupo deportivo identificado por `grupo` y `temporada`. Un equipo puede tener hasta 25 jugadores.
  
* **Gestor:** Perfil derivado de Usuario.

* **Jugador:** Perfil derivado de Usuario, con el atributo propio de 'fechaNacimiento' y atributos derivados de usurio. Realiza pagos, juega en equipos, asiste a sesiones de entrenamiento.

* **Pago:** Registro asociado a un Jugador que recoge `importe` y `fecha`. El pago mensual debe estar realizado para que el jugador participe en el entrenamiento.

* **Participación:** Clase de asociación entre Jugador y SesionEntrenamiento que registra `fechaAcude` y `Rendimiento`. El rendimiento debe estar entre 0 y 10.

* **SesionEntrenamiento:** Sesión con `fechaHoraInicio` y `fechaHoraFin`, relacionada con un equipo ,con las participaciones de los jugadores y se realiza en un campo.

* **Usuario:** Clase base con los atributos `email` ,`contraseña` , `nombre` y `telefono`. La especialización en Jugador y Gestor es completa y disjunta: todo Usuario pertenece a uno de esos dos tipos.

## 3. Visión general del sistema

### 3.1. Requisitos generales

El sistema de gestión de la academia de fútbol administra usuarios, equipos, entrenamientos, pagos y campos deportivos. El modelo conceptual establece las siguientes relaciones y restricciones:

* **Gestión de usuarios:** Usuario se especializa en Jugador y Gestor mediante una jerarquía completa y disjunta. Ambos perfiles comparten las credenciales `email` y `contraseña`.

* **Control de pagos:** Cada Pago registra el `importe` y la `fecha`, y está asociado a un Jugador. El pago mensual debe estar realizado para que el jugador participe en los entrenamientos.

* **Gestión de equipos:** Equipo se identifica mediante `grupo` y `temporada`. Los jugadores juegan en equipos y cada equipo tiene un máximo de 25 jugadores.

* **Gestión de entrenamientos:** Las sesiones registran `fechaHoraInicio` y `fechaHoraFin`. La participación de cada jugador en una sesión se registra mediante la clase de asociación Participación, con `fechaAcude` y `Rendimiento`.

* **Gestión de campos:** El Gestor alquila los campos deportivos.

* **Evaluación deportiva:** El rendimiento de cada jugador en una sesión debe estar entre 0 y 10.

### 3.2. Usuarios del sistema

El sistema distingue dos tipos de usuarios: Jugador y Gestor. Ambos heredan de Usuario, que almacena `email` y `contraseña`. La especialización es completa y disjunta, por lo que todo Usuario pertenece a uno de esos perfiles.

| **Tipo de actor** | **Rol / perfil** | **Descripción** |
| :--- | :--- | :--- |
| **Jugador** | Alumno de la academia | Tiene los atributos `nombre`, `fechaNacimiento` y `telefono`. Realiza pagos, juega en equipos y participa en sesiones de entrenamiento. |
| **Gestor** | Responsable administrativo | Tiene los atributos `nombre` y `telefono`. Se encarga de alquilar campos y gestionar la actividad de la academia. |

## 4. Catálogo de requisitos

### 4.1. Requisitos funcionales

### R.F.01. Registrar los pagos de un jugador

**Como** Gestor

**Quiero** registrar el importe y la fecha de los pagos de cada jugador

**Para** controlar el abono mensual de la academia.

**Prueba de aceptación**

* Registrar para cada Pago el `importe` y la `fecha`.
* Asociar cada pago con el Jugador correspondiente.
* Comprobar que el jugador ha realizado el pago mensual antes de permitirle participar en el entrenamiento.

---

### R.F.02. Gestionar los equipos y sus jugadores

**Como** Gestor

**Quiero** gestionar los equipos por grupo y temporada

**Para** organizar a los jugadores de la academia.

**Prueba de aceptación**

* Registrar el `grupo` y la `temporada` de cada Equipo.
* Asociar los jugadores con sus equipos.
* Comprobar que un equipo no supere el máximo de 25 jugadores.

---

### R.F.03. Registrar sesiones y participaciones

**Como** Gestor

**Quiero** registrar las sesiones de entrenamiento y la participación de cada jugador

**Para** llevar el control de la asistencia y del rendimiento deportivo.

**Prueba de aceptación**

* Registrar para cada sesión la `fechaHoraInicio` y la `fechaHoraFin`.
* Asociar las sesiones con los equipos correspondientes.
* Registrar la participación de cada Jugador en cada sesión mediante la clase de asociación Participación.
* Guardar en cada Participación la `fechaAcude` y el `Rendimiento`.
* Validar que el `Rendimiento` esté entre 0 y 10.
* Comprobar que el jugador haya realizado el pago mensual antes de participar.

---

### R.F.04. Alquilar campos deportivos

**Como** Gestor

**Quiero** alquilar campos deportivos

**Para** disponer de instalaciones para la actividad de la academia.

**Prueba de aceptación**

* Asociar los campos alquilados con el Gestor.
* Registrar y consultar los tres atributos del Campo (`Item 1`, `Item 2` e `Item 3`), cuyos nombres aparecen así en el modelo conceptual.

---

## 4.1.1. Requisitos de información

#### R.I.01. Datos de usuario

**Como** Gestor

**Quiero** guardar las credenciales de los usuarios

**Para** que puedan identificarse en el sistema.

**Prueba de aceptación**

* Guardar el `email` y la `contraseña` de cada Usuario.
* Comprobar que Usuario se especializa en Jugador y Gestor mediante una jerarquía completa y disjunta.

---

#### R.I.02. Datos del jugador

**Como** Gestor

**Quiero** guardar los datos de los jugadores

**Para** gestionar su participación en la academia.

**Prueba de aceptación**

* Guardar el `nombre`, la `fechaNacimiento` y el `telefono`.
* Incluir las credenciales heredadas de Usuario.
* Asociar al jugador con sus pagos, equipos y participaciones en sesiones.

---

#### R.I.03. Datos del gestor

**Como** Gestor

**Quiero** guardar mis datos de perfil

**Para** realizar las gestiones de la academia.

**Prueba de aceptación**

* Guardar el `nombre` y el `telefono`.
* Incluir las credenciales heredadas de Usuario.
* Asociar al Gestor con los campos que alquila.

---

#### R.I.04. Datos del equipo

**Como** Gestor

**Quiero** guardar la información de los equipos

**Para** organizarlos por grupo y temporada.

**Prueba de aceptación**

* Guardar el `grupo` y la `temporada`.
* Asociar el Equipo con sus jugadores.
* Respetar el máximo de 25 jugadores por equipo.

---


#### R.I.05. Datos de la sesión de entrenamiento

**Como** Gestor

**Quiero** guardar los datos de las sesiones

**Para** organizar los entrenamientos de los equipos.

**Prueba de aceptación**

* Guardar `fechaHoraInicio` y `fechaHoraFin`.
* Asociar las sesiones con los equipos.
* Registrar las participaciones de los jugadores en cada sesión.

---

#### R.I.08. Datos de participación y rendimiento

**Como** Gestor

**Quiero** guardar la asistencia y el rendimiento de cada jugador en las sesiones

**Para** consultar su actividad deportiva.

**Prueba de aceptación**

* Guardar `fechaAcude` y `Rendimiento` en la clase de asociación Participación.
* Asociar cada Participación con un Jugador y una SesionEntrenamiento.
* Validar que `Rendimiento` esté entre 0 y 10.

---

#### R.I.09. Datos del pago

**Como** Gestor

**Quiero** guardar los datos de los pagos de los jugadores

**Para** controlar el abono mensual.

**Prueba de aceptación**

* Guardar `importe` y `fecha`.
* Asociar cada Pago con el Jugador correspondiente.
* Comprobar que el pago mensual esté realizado antes de la participación del jugador en el entrenamiento.

---

#### R.I.10. Datos del campo

**Como** Gestor

**Quiero** guardar los datos de los campos deportivos

**Para** gestionar su alquiler.

**Prueba de aceptación**

* Asociar cada Campo con el Gestor que lo alquila.
* Registrar y consultar los atributos `Item 1`, `Item 2` e `Item 3`, tal como aparecen en el modelo conceptual.

---

### 4.1.2. Reglas de negocio

#### R.N.01. Pago mensual para participar

El pago mensual debe estar realizado para que un Jugador participe en el entrenamiento.

#### R.N.02. Rango del rendimiento

El valor de `Rendimiento` registrado en una Participación debe estar entre 0 y 10.

#### R.N.03. Pago corriente

No se puede introducir una sesión de entrenamiento si el jugador no tiene el pago corriente de ese mes

#### R.N.04. Participación en Sesion de Entrenamiento

Un jugador no puede participar en una sesión de entrenamiento a la que no pertenece

---

## 4.2. Mapa de historias de usuario

| ID Historia | Rol / Actor | Servicio / Acción | Requisito relacionado | Regla de negocio |
| :--- | :--- | :--- | :--- | :--- |
| **HU-01** | Gestor | Registrar y consultar los pagos de los jugadores | R.F.01, R.I.09 | R.N.01 |
| **HU-02** | Gestor | Organizar equipos y asignarles jugadores por grupo y temporada (máximo 25 por equipo) | R.F.02, R.I.04 | - |
| **HU-03** | Gestor | Registrar sesiones de entrenamiento asociadas a un equipo y a un campo | R.F.03, R.I.05 | R.N.03 |
| **HU-04** | Gestor | Registrar la asistencia y el rendimiento de cada jugador en las sesiones | R.F.03, R.I.08 | R.N.01, R.N.02, R.N.04 |
| **HU-05** | Gestor | Alquilar y gestionar los campos deportivos | R.F.04, R.I.10 | - |
| **HU-06** | Gestor | Gestionar los datos de los usuarios (jugadores y gestor) y sus credenciales | R.I.01, R.I.02, R.I.03 | - |

## 4.3. Requisitos no funcionales (opcional)

### R.N.F. 01. Guardar contraseñas de forma segura
Como Jugador / Gestor quiero que mi clave se guarde encriptada en la base de datos para que nadie pueda robármela.

### R.N.F. 02. Control automático de fallos en los datos
Como Gestor quiero que el sistema me avise o me bloquee si pongo mal una nota o un contrato para no guardar datos incorrectos por descuido.


-- fin entregable 1 --

## 5. Modelo conceptual

### 5.1. Diagrama de clases UML

<img width="1302" height="752" alt="modelo_conceptual_club_1 drawio" src="https://github.com/user-attachments/assets/fe4e9210-c533-4400-8507-aa3065f64054" />

Escenario 1: Asignación válida de participación y rendimiento
Descripción textual: Un gestor registra un equipo "Alevín A" (Temporada 2025/2026) con el jugador "Carlos Gómez". Carlos ha realizado el pago correspondiente a Noviembre de 2026. Se crea una sesión de entrenamiento para el 10/11/2026 en el "Campo Municipal" (Estado: activo). Carlos asiste y el gestor le asigna un rendimiento de 8.5. Se cumplen todas las restricciones (R01, R02, R03, R04).


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


