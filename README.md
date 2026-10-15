# ACADEMIA DE FÚTBOL "Gol & Formación"
 
## Miembros del grupo L6-DF-8 

1. Urbano Castro, Ignacio
1. Lorenzo Raposo, Daniel
1. Romero Gómez, Rafael
1. Camargo Moral, Julian

## 1. Introducción al problema

La Academia de Fútbol "Gol & Formación" ha experimentado un crecimiento en su volumen de alumnos durante los últimos años. Lo que comenzó como una pequeña escuela y equipo local ha evolucionado hasta convertirse en un reconocido club deportivo. En la actualidad, la institución centra su actividad exclusivamente en la vertiente formativa y deportiva.

Gestión Deportiva y Académica: Coordinación de equipos federados y de escuela en distintas categorías de edad (desde Prebenjamín hasta Juvenil), supervisión del cuerpo técnico, planificación de   sesiones de entrenamiento en pistas específicas y control de cuotas mensuales de los alumnos. 



## 2. Glosario de términos

Los términos específicos empleados en el dominio del problema son los siguientes:

* **Campo:** Instalación deportiva gestionada por el Gestor en la que se desarrollan los entrenamientos de la academia.

* **Gestor:** Perfil administrativo derivado de la clase Usuario, encargado del alquiler de campos y la supervisión operativa del club.
  
* **Participación:** Clase de asociación entre Jugador y Sesión de Entrenamiento que registra la asistencia física (fechaAcude) y la evaluación deportiva (Rendimiento).

* **Rendimiento:** Calificación cuantitativa asignada a un jugador en una sesión de entrenamiento, acotada estrictamente en el rango de 0 a 10.

* **Usuario:** Clase base abstracta de la que heredan obligatoriamente Jugador y Gestor {completa, disjunta}, encargada de almacenar las credenciales de acceso (email y contraseña).



## 3. Visión general del sistema

### 3.1. Requisitos generales


El sistema de gestión de la academia de fútbol se basa en la gestión administrativa y de instalaciones. Los requisitos generales que definen el alcance del sistema son los siguientes:

* **Gestión de Usuarios:** Implementación de una arquitectura de usuarios jerárquica `{completa, disjunta}` basada en la entidad base **Usuario** (credenciales de `email` y `contraseña`), especializándose de manera exclusiva en los perfiles **Jugador** y **Gestor**.

* **Control de Acceso (R01):** Verificación del cumplimiento del abono mensual (Pago: `importe`, `fecha`) por parte del Jugador como requisito indispensable para quedar habilitado y participar en las sesiones de entrenamiento.

* **Gestión de Plantillas (R02):** Administración de los equipos (Equipo: `grupo`, `temporada`) y supervisión estricta de la relación con los jugadores, garantizando que un equipo no supere el límite máximo de 25 jugadores.
  
* **Gestión del Cuerpo Técnico (R03):** Registro y control de la vinculación entre entrenadores y equipos mediante la entidad intermedia Contrato (`fechaInicio`, `fechaFin`), limitando la duración máxima de cada contrato a 1 año.
  
* **Planificación Deportiva (R03):** Programación de sesiones de entrenamiento (SesionEntrenamiento: `fechaHoraInicio`, `fechaHoraFin`) y registro individualizado del rendimiento del jugador a través de la clase de asociación Partición (`fechaAcude`, `Rendimiento`), asegurando que las calificaciones se mantengan estrictamente en el rango numérico de 0 a 10.
  
* **Administración de Instalaciones:** Gestión del catálogo de campos deportivos (Campo) por parte del perfil Gestor , permitiendo su control.



### 3.2. Usuarios del sistema

Nuestro sistema clasifica a los usuarios que interactúan directamente con la plataforma mediante una jerarquía de herencia completa y disjunta derivada de la clase base abstracta Usuario.

La entidad base Usuario es la encargada de almacenar las credenciales de acceso al sistema (email y contraseña). De esta clase abstracta se derivan de forma obligatoria y exclusiva {completa, disjunta} los dos únicos perfiles con acceso a la plataforma: el Jugador y el Gestor. Esta arquitectura garantiza que todo usuario en el sistema pertenezca estrictamente a uno de estos dos tipos.

| **Tipo de Actor** | **Rol / Perfil** | **Descripción y Situación Actual** | **Expectativas del Nuevo Sistema** |
| :--- | :--- | :--- | :--- |
| **Usuario** | Jugador | Alumno inscrito en la escuela formativa que pertenece a una categoría concreta y realiza el abono periódico de las cuotas mensuales. | Transparencia total en el estado de sus pagos/cuotas, asignación garantizada de sus horarios y campos de entrenamiento, y correcta categorización por edad. |
| **Gestor** | Directivo de la academia | Encargado de la gestión global de la academia, del alquiler de los campos donde se realizan las sesiones de entrenamiento. | Disponer de un panel centralizado para gestionar altas de jugadores, automatizar el control de cobros e impagos, asignar pistas sin solapamientos y supervisar los cupos por equipo.. |

## 4. Catálogo de requisitos

# 4. Catálogo de requisitos

## 4.1. Requisitos funcionales

### R.F.01. Meter un jugador en un equipo
**Como** Gestor

**Quiero** apuntar y vincular a un jugador dentro de un equipo 

**Para** ir formando la plantilla de la temporada.

**Prueba de aceptación**
* Comprobar que el jugador existe en el sistema y elegir el equipo indicando su grupo y su temporada.
* Ver cuántos jugadores hay ya apuntados en el equipo antes de confirmar la entrada.
* Validar que la categoría de edad del jugador coincida con el rango admitido por el equipo, grupo y temporada seleccionados.
* Permitir buscar al jugador en el sistema mediante filtros rápidos por DNI, nombre completo o número de ficha.
* Comprobar que el sistema no permita vincular de forma duplicada al mismo jugador en el mismo equipo y temporada.
* Mostrar una advertencia o alerta si el equipo alcanza o supera el cupo máximo de plantilla configurado.
* Asignar de forma automática el estado "Activo" a la vinculación del jugador tras confirmar el registro.
* Registrar la fecha, la hora y el usuario gestor que realizó la asignación en el módulo de auditoría.
* Permitir cancelar la operación de vinculación en cualquier momento previo a la confirmación sin guardar cambios.
* Visualizar un mensaje de confirmación con el resumen de la plantilla actualizada tras guardar el registro.
  

---

### R.F.02. Apuntar asistencia y nota del entrenamiento
**Como** Gestor 

**Quiero** registrar si un jugador ha venido a la sesión de entrenamiento

**Para** calcular su nota de rendimiento.

**Prueba de aceptación**
* Comprobar que el jugador tiene pagada la cuota de ese mes antes del entrenamiento.
* Ver que la nota que le ponemos se quede guardada correctamente en su ficha del entrenamiento (`Partición`).
* Se debe aplicar la regla de negocio **R.N.01**.
* Se debe aplicar la regla de negocio **R.N.04**.
* Permitir registrar el estado de asistencia individual o masivo (Asiste, Falta Justificada, Falta Injustificada).
* Bloquear el registro de notas o mostrar una alerta visible si el sistema detecta cuotas o pagos adeudados.
* Verificar que la nota registrada quede vinculada de forma unívoca a la sesión de entrenamiento y a la fecha correspondiente.
* Ofrecer un campo de observaciones cualitativas opcional para anotaciones del cuerpo técnico sobre el desempeño.
* Guardar la identidad del usuario (gestor o técnico) y la marca de tiempo del registro o última modificación realizada.
* Permitir la modificación o corrección de la nota únicamente dentro del plazo temporal permitido por la normativa.

---

### R.F.03. Hacer el contrato de un entrenador
**Como** Gestor 

**Quiero** guardar el contrato de un entrenador con un equipo 

**Para** asignarle oficialmente su grupo.

**Prueba de aceptación**
 * Elegir un entrenador y un equipo poniendo la fecha en que empieza y en la que termina el contrato.
 * Comprobar que el sistema revise las fechas y no deje poner un periodo más largo de lo permitido.
 * Validar que la fecha de inicio del contrato sea strictly anterior a la fecha de finalización.
 * Comprobar que el entrenador seleccionado esté dado de alta previamente y con estado activo en el sistema.
 * Alertar e impedir el registro si el entrenador posee un contrato activo e incompatible en las mismas fechas para otro equipo.
 * Permitir adjuntar o asociar el archivo digitalizado del contrato firmado (en formato PDF o imagen) al registro.
 * Consultar los datos del contrato vigente tanto desde la ficha del entrenador como desde la gestión del equipo.
 * Permitir la edición o actualización de los datos del contrato previo a su firma o activación definitiva.
 * Cambiar de manera automática el estado del contrato a "Finalizado" una vez rebasada la fecha de término indicada.
 * Guardar en la auditoría del sistema la fecha, la hora y el usuario gestor responsable del alta del contrato.
---

### R.F.04. Ver si el pago está al día
**Como** Jugador 

**Quiero** mirar mis pagos pasados y saber si tengo la cuota al mes 

**Para** estar seguro de que puedo ir a entrenar.

**Prueba de aceptación**
* Entrar a la app y ver la lista de pagos de mi propia cuenta.
* Ver cada recibo con el dinero pagado y la fecha en que se hizo.
* Visualizar un indicador gráfico o estado general claro de la cuenta (por ejemplo, "Al día" o "Cuota pendiente").
* Consultar el detalle de cada recibo con su concepto (cuota mensual, matrícula, equipación) y método de pago utilizado.
* Mostrar la fecha límite de vencimiento de las cuotas o cobros pendientes de pago.
* Permitir filtrar y ordenar el historial de recibos por estado (Pagado, Pendiente) o por temporada deportiva.
* Garantizar que un jugador solo pueda consultar sus propios datos de pago y nunca los de otros miembros.
* Permitir la descarga o generación en formato PDF del comprobante de pago de cada recibo abonado.
* Actualizar el estado de los pagos en la app en tiempo real una vez que la administración valida una transacción.
* Recibir notificaciones en la aplicación sobre el vencimiento próximo de las cuotas mensuales.

---

### R.F.05. Ver mi asistencia y mis notas
**Como** Jugador 

**Quiero** ver a qué entrenos he ido y qué notas me han puesto 

**Para** saber cómo voy en el equipo.

**Prueba de aceptación**
* Entrar al historial de entrenamientos a los que he asistido.
* Ver en cada entrenamiento el día que fui (`fechaAcude`) y la nota que me puso el cuerpo técnico (`Rendimiento`).
* Presentar la lista de entrenamientos ordenada cronológicamente desde la sesión más reciente hasta la más antigua.
* Consultar las observaciones u anotaciones cualitativas adicionales que el entrenador haya registrado.
* Distinguir mediante etiquetas o colores el estado de asistencia marcado (Asistió, Falta Justificada, Falta Injustificada).
* Calcular y mostrar la nota media o promedio acumulado del rendimiento del jugador en el mes o temporada.
* Permitir filtrar la lista de entrenamientos y evaluaciones por rangos de fechas o meses concretos.
* Asegurar que la pantalla sea de solo lectura para evitar cualquier intento de modificación de notas o asistencias.
* Recibir una notificación en la aplicación cada vez que el cuerpo técnico publique las notas de una sesión.
* Permitir la visualización resumida o exportación del informe de asistencia y rendimiento del jugador.

---

### R.F.06. Guardar y organizar los campos de fútbol
**Como** Gestor 

**Quiero** dar de alta y cambiar los datos de los campos de fútbol 

**Para** organizar los espacios de entreno.

**Prueba de aceptación**
* Guardar los datos de identificación del campo deportivo.
* Ver la lista completa de campos que gestiona el club.
* Editar y actualizar cualquier dato descriptivo previamente registrado en la ficha del campo deportivo.
* Validar que el sistema no permita registrar dos campos deportivos con el mismo nombre o código identificador.
* Registrar especificaciones técnicas de la instalación (tipo de superficie: césped natural, artificial; iluminación; vestuarios).
* Modificar y visualizar el estado de operatividad del campo (Disponible, En Mantenimiento, Inhabilitado).
* Definir la disponibilidad horaria y los días de la semana habilitados para el uso y reserva de cada campo.
* Bloquear la eliminación o desactivación de un campo deportivo si tiene entrenamientos o partidos asignados activos.
* Permitir la búsqueda y filtrado de la lista de campos por nombre, tipo de superficie o disponibilidad.
* Registrar en el historial de auditoría el usuario gestor, la fecha y la hora de cada alta o modificación realizada.

---

### 4.1.1. Requisitos de información

#### R.I.01. Datos de usuario y login
Como Gestor quiero guardar el correo y la clave de cada persona para que puedan entrar a la app de forma segura.

**Prueba de aceptación**
* Comprobar que sea obligatorio poner `email` y `contraseña`.
* Ver que cada cuenta creada sea obligatoriamente de tipo `Jugador` o `Gestor`.

#### R.I.02. Ficha del jugador
Como Gestor quiero guardar los datos de los futbolistas para tener la lista completa de los jugadores de la academia.

**Prueba de aceptación**
* Comprobar que se guardan el `nombre`, `fechaNacimiento` y `telefono`.
* Comprobar que incluye los datos de inicio de sesión por ser un tipo de `Usuario`.

#### R.I.03. Ficha del gestor
Como Gestor quiero guardar mis datos de contacto para saber quién hace las gestiones administrativas.

**Prueba de aceptación**
* Comprobar que se guardan el `nombre` y `telefono`.
* Comprobar que incluye los datos de inicio de sesión por ser un tipo de `Usuario`.

#### R.I.04. Datos del equipo
Como Gestor quiero guardar la información de los equipos para tenerlos organizados por grupos y años.

**Prueba de aceptación**
* Comprobar que se guardan el `grupo` y la `temporada`.
* Ver que el equipo queda bien conectado con sus jugadores y sus entrenadores.

#### R.I.05. Datos del entrenador
Como Gestor quiero guardar la información del entrenador para saber a quién contratamos en el club.

**Prueba de aceptación**
* Comprobar que se apuntan el `nombre`, `telefono` y `DNI`.
* Confirmar que es un dato que maneja el Gestor y que el entrenador no tiene cuenta para entrar a la app.

#### R.I.06. Datos del contrato
Como Gestor quiero guardar las fechas del contrato del entrenador para saber cuándo empieza y cuándo termina su trabajo.

**Prueba de aceptación**
* Comprobar que se guardan la `fechaInicio` y `fechaFin` al unir al entrenador con el equipo.


#### R.I.07. Horarios del entrenamiento
Como Gestor quiero guardar los horarios de los entrenamientos para organizar la agenda del club.

**Prueba de aceptación**
* Comprobar que se guardan la `fechaHoraInicio` y la `fechaHoraFin`.
* Ver a qué equipo le toca entrenar en esa hora.

#### R.I.08. Datos de asistencia y notas (Partición)
Como Gestor quiero guardar si el jugador fue al entreno y su nota para saber cómo evoluciona en el campo.

**Prueba de aceptación**
* Comprobar que se guarda el día que fue (`fechaAcude`) y la nota obtenida (`Rendimiento`).


#### R.I.09. Datos del pago
Como Gestor quiero guardar los cobros de las cuotas para saber quién ha pagado y quién debe dinero.

**Prueba de aceptación**
* Comprobar que se guardan el `importe` (dinero) y la `fecha` del pago.
* Ver a qué jugador le pertenece ese recibo.

---

### 4.1.2. Reglas de negocio

#### R.N.01. Hay que pagar para entrenar
El pago mensual deberá estar realizado por el jugador para participar en el entrenamiento.

#### R.N.02. Límite de jugadores en el equipo
Un equipo tendrá un máximo de 25 jugadores.

#### R.N.03. Duración máxima del contrato
Los contratos tendrán una duración máxima de 1 año.


---

## 4.2. Mapa de historias de usuario (opcional)

| ID Historia | Rol / Actor | Servicio / Acción | R.F. Relacionado | Regla de Negocio |
| :--- | :--- | :--- | :---: | :---: |
| **HU-01** | Gestor | Dar de alta y cambiar datos de los campos de fútbol | R.F.06 | - |
| **HU-02** | Gestor | Hacer el contrato del entrenador para un equipo | R.F.03 | R.N.03 |
| **HU-03** | Gestor | Apuntar jugadores en las plantillas de los equipos | R.F.01 | R.N.02 |
| **HU-04** | Jugador | Ver los pagos hechos y saber si la cuota está al día | R.F.04 | R.N.01 |
| **HU-05** | Jugador | Ver los entrenos a los que ha ido y sus notas | R.F.05 | R.N.04 |
| **HU-06** | Gestor | Apuntar la asistencia y poner la nota en un entreno | R.F.02 | R.N.01, R.N.04 |

---

## 4.3. Requisitos no funcionales (opcional)

### R.N.F. 01. Guardar contraseñas de forma segura
Como Jugador / Gestor quiero que mi clave se guarde encriptada en la base de datos para que nadie pueda robármela.

### R.N.F. 02. Control automático de fallos en los datos
Como Gestor quiero que el sistema me avise o me bloquee si pongo mal una nota o un contrato para no guardar datos incorrectos por descuido.


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


