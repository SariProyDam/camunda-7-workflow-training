# Despliegue del proceso

## 🎯 Objetivo

Mover el modelo BPMN al directorio donde **Camunda lo desplegará automáticamente** y verificar que el proceso aparece en el motor.

---

## 🧠 Contexto

Durante los ejercicios anteriores los modelos BPMN se han guardado en:

```
model/
```

Este directorio sirve para **editar y versionar los modelos**, pero el motor Camunda no lo escanea automáticamente.

Camunda despliega automáticamente los procesos que se encuentran en:

```
src/main/resources/processes
```

Por lo tanto, para que el motor pueda ejecutar el proceso es necesario copiar el modelo a ese directorio.

---

# Copiar el modelo BPMN al backend

Abre una **terminal**. Desde la **raíz del repositorio** (donde están **labs**, **backend** y **model**) ejecuta:

```bash
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Verificar que el archivo se ha copiado

Ejecutar:

```bash
ls backend/src/main/resources/processes
```

Debería aparecer el archivo:

```
approval-process.bpmn
```

---

# Arrancar la aplicación

En la terminal, desde la raíz del repo: `cd backend`. Luego arranca la aplicación:

```bash
mvn spring-boot:run
```

Durante el arranque el motor Camunda escaneará el directorio `processes`.

Si encuentra modelos BPMN, los desplegará automáticamente.

---

# Verificar el despliegue en Cockpit

Abre el **navegador** y ve a **http://localhost:8081/camunda** (o el puerto que use tu aplicación; lo ves en la terminal al arrancar). Inicia sesión si lo pide. Dentro de la interfaz de Camunda, en el **menú o la barra lateral** haz clic en **Cockpit** (o en **Processes** si ya estás en Cockpit).

Debería aparecer el proceso:

```
approval-process
```

---

# Explorar el proceso desplegado

Haz **clic** en el proceso **approval-process** en la lista. Camunda mostrará para ese proceso:

* el diagrama BPMN
* las estadísticas del proceso
* instancias activas
* historial de ejecución

Esto confirma que el proceso ha sido desplegado correctamente.

---

# Qué ha ocurrido

Cuando la aplicación arranca:

```
Spring Boot inicia
        │
        ▼
Camunda escanea resources/processes
        │
        ▼
Se despliegan los modelos BPMN
        │
        ▼
Los procesos quedan disponibles en el motor
```

---

# Comprobación

El ejercicio se considera completado cuando:

* el archivo BPMN se copia a `resources/processes`
* la aplicación arranca correctamente
* el proceso aparece en **Camunda Cockpit**.
