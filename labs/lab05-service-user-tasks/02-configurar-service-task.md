# Configurar la Service Task

## 🎯 Objetivo

Configurar la **Service Task** del modelo BPMN para que ejecute la clase Java creada en el ejercicio anterior.

---

## 🧠 Contexto

En el ejercicio anterior se creó una clase:

```id="5tdh7a"
ValidarSolicitudDelegate
```

Esta clase implementa:

```id="b98sna"
JavaDelegate
```

Ahora es necesario indicar en el modelo BPMN que la **Service Task** debe ejecutar esa clase cuando el proceso llegue a ese punto.

Esto se hace configurando el atributo:

```id="p6k3sh"
Delegate Expression
```

---

# Abrir el modelo BPMN

Abre **model/approval-process.bpmn** en **Camunda Modeler** (File → Open, carpeta model del repo).

---

# Seleccionar la Service Task

En el diagrama, **haz clic** en la tarea **Validar solicitud**. En el **panel de propiedades a la derecha** (si no lo ves, Window → Show Properties) se mostrarán las opciones de esa tarea.

---

# Configurar el tipo de implementación

En el panel de propiedades busca la sección **Implementation** (o "Implementación"). En el tipo de implementación elige **Delegate Expression**.

---

# Configurar la expresión del delegate

En el campo que aparezca para la expresión (suele ser "Delegate Expression" o similar), escribe:

```
${validarSolicitudDelegate}
```

Esto indica al motor Camunda que debe ejecutar el **bean Spring** correspondiente a esa clase.

El nombre del bean se genera automáticamente a partir del nombre de la clase:

```
ValidarSolicitudDelegate
```

↓

```
validarSolicitudDelegate
```

---

# Guardar el modelo

Guardar los cambios en el archivo:

```
model/approval-process.bpmn
```

---

# Copiar el modelo al backend

Desde la **raíz del repositorio** (donde están **labs**, **backend** y **model**) ejecuta en la terminal:

```bash
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Ejecutar la aplicación

En la terminal, `cd backend` (desde la raíz del repo) y luego ejecuta:

```bash
mvn spring-boot:run
```

---

# Verificar la ejecución del delegate

Cuando el proceso se ejecute, el motor llamará al método:

```java
execute()
```

de la clase:

```
ValidarSolicitudDelegate
```

En la consola debería aparecer el mensaje:

```
Ejecutando validación automática de la solicitud
```

---

# Qué ha ocurrido

El flujo ahora funciona de la siguiente forma:

```
Inicio
   │
   ▼
Service Task (Validar solicitud)
   │
   ▼
Ejecuta ValidarSolicitudDelegate
   │
   ▼
Aprobar solicitud
   │
   ▼
Fin
```

---

# Comprobación

El ejercicio se considera completado cuando:

* la Service Task tiene configurado un **Delegate Expression**
* el modelo BPMN se actualiza en `resources/processes`
* al ejecutar el proceso se llama a `ValidarSolicitudDelegate`.
