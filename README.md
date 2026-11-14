# UNIDAD-3-BASE-DE-DATOS-EJERCICIO-17
Este diagrama entidad-relación (o modelo relacional) representa la estructura lógica de una **base de datos para la gestión de una clínica veterinaria**, diseñada para administrar los titulares (propietarios), las mascotas (pacientes), el historial clínico, el control de vacunas y el personal médico.

A continuación se detalla qué representa cada tabla y cómo se relacionan entre sí:

### 1. Entidades Principales (Tablas)

* **`TITULAR`**: Almacena la información de los dueños o responsables legales de las mascotas.


* *Campos:* `DNI` (Clave Primaria), `NOMBRE`, `APELLIDO`, `CORREO` y `TELEFONO`.




* **`MASCOTA`**: Contiene el registro de los animales pacientes atendidos en la clínica.


* *Campos:* `NUM_HISTORIA_CLINICA` (Clave Primaria), `NOMBRE`, `COLOR`, `ESPECIE`, `RAZA`, `SEXO` y mantiene una relación con su titular.




* **`VACUNA`**: Almacena el catálogo de inmunizaciones disponibles.


* *Campos:* `COIDOG_VACUNA` (Clave Primaria, nota de tipeo en el gráfico), `NUM_LOTE`, `NOMBRE_COMERCIAL` y `LABORATORIO`.




* **`REGISTRO_APLICACION_VACUNA`**: Tabla intermedia que resuelve la relación de muchos a muchos (N:M) entre mascotas y vacunas.


* *Campos:* `NUM_HISTORIA_CLINICA` y `COIDOG_VACUNA` (ambas forman la Clave Primaria compuesta y actúan como Claves Foráneas), junto con `FECHA_APLICACION` y `FECHA_REFUERZO`.




* **`CONSULTA`**: Registra el historial de las atenciones médicas y evoluciones clínicas.


* *Campos:* `ID_CONSULTA` (Clave Primaria), `FECHA`, `HORA`, `PESO`, `DIAGNOSTICO`, `TEMPERATURA_CORPORAL`, `NUM_HISTORIA_CLINICA` (Clave Foránea hacia la mascota) y `MATRICULA_PROFESIONAL` (Clave Foránea hacia el veterinario).




* **`VETERINARIO`**: Contiene los datos del personal médico de la clínica.


* *Campos:* `MATRICULA_PROFESIONAL` (Clave Primaria), `NOMBRE`, `APELLIDO`, `ESPECIALIDAD` y `TELEFONO`.





---

### 2. Relaciones Principales

* **Titular y Mascotas:** Un propietario (`TITULAR`) puede tener una o varias mascotas registradas, pero cada paciente pertenece a un único dueño (relación de 1 a N).


* **Historial de Vacunación:** Permite llevar el control detallado de qué vacunas se le han aplicado a cada mascota y cuándo corresponden sus refuerzos a través de la tabla intermedia.


* **Atención Médica:** Cada consulta clínica vincula a una mascota específica con el veterinario responsable que la atendió, registrando los signos vitales y el diagnóstico de la visita.
<img width="1362" height="762" alt="EJERCICIO 17-MR drawio" src="https://github.com/user-attachments/assets/6acd7930-5925-47c6-abac-27f2e4a35cdd" />

Este diagrama muestra el **proceso completo de normalización de bases de datos** aplicado a un sistema de gestión para una clínica veterinaria, transformando una estructura inicial desnormalizada (Forma Normal 0) hasta llegar al diseño relacional optimizado en Tercera Forma Normal (3FN).

A continuación se detalla cada una de las fases representadas:

### 1. Fase Normal 0 (FN0) — Tabla No Normalizada

* Se parte de una **única tabla masiva y plana** que concentra toda la información mezclada en una sola estructura: datos de los pacientes (mascotas), sus dueños (propietarios) y dos grupos repetitivos con colecciones de datos anidados dentro de celdas: la lista de vacunas aplicadas y el historial de consultas médicas.


* **Problema:** Contiene grupos multivaluados y datos anidados, lo que provoca una alta redundancia de información y dificulta cualquier operación de actualización, consulta o mantenimiento del sistema.



---

### 2. Primera Forma Normal (1FN)

* Se eliminan los grupos repetitivos y se asegura que **todos los atributos sean atómicos** (cada celda contiene un único valor), expandiendo los registros para que cada fila represente una combinación individual y libre de valores anidados.


* Se obtiene una tabla tabular plana (`TABLA PLANTILLA`) donde cada campo es indivisible, definiéndose claves primarias compuestas, aunque todavía persiste una alta duplicidad de datos en la información de las mascotas, los dueños y los veterinarios.



---

### 3. Segunda Forma Normal (2FN)

* Se parte de la 1FN y se eliminan las **dependencias parciales**. Se separan los atributos basándose en sus claves principales correspondientes, desglosando la información en cinco tablas independientes y normalizadas:


* **`TABLA MASCOTA`**: Almacena el registro de los animales de compañía y sus características físicas.


* **`TABLA VACUNA`**: Contiene el catálogo de vacunas disponibles y sus laboratorios.


* **`TABLA REGISTRO_APLICACION_VACUNA`**: Tabla intermedia que vincula las mascotas con las vacunas aplicadas y sus fechas de refuerzo.


* **`TABLA CONSULTA`**: Registra el historial clínico, pesos, diagnósticos y temperaturas de las atenciones médicas.


* **`TABLA TITULAR`**: Gestiona la información personal de los dueños de las mascotas.





---

### 4. Tercera Forma Normal (3FN)

* Se eliminan las **dependencias transitivas**, garantizando que ningún atributo no clave dependa de otro atributo no clave. El diseño se consolida en un modelo relacional robusto y totalmente normalizado, interconectado mediante claves foráneas (FK), lo que asegura la integridad referencial y evita anomalías para la clínica veterinaria:


* **`TABLA TITULAR`**: Administra los datos de los dueños.


* **`TABLA MASCOTA`**: Mantiene el inventario de pacientes.


* **`TABLA VACUNA`**: Catálogo de inmunizaciones.


* **`TABLA VETERINARIO`**: Tabla incorporada que centraliza los datos del personal médico (matrícula, nombre, especialidad, teléfono), evitando duplicidades en las consultas.


* **`TABLA REGISTRO_APLICACION_VACUNA`**: Historial de vacunación.


* **`TABLA CONSULTA`**: Detalle de las atenciones clínicas asociadas al veterinario correspondiente mediante su clave foránea.
<img width="4582" height="2922" alt="EJERCICIO 17-FASES DE NORMALIZACION drawio" src="https://github.com/user-attachments/assets/3be52268-0d83-40f9-a073-1f9d7945bf9f" />

