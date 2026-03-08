# Añadir una Service Task

## 🎯 Objetivo

Modificar el modelo BPMN para añadir una **Service Task**, que representa una tarea ejecutada automáticamente por el sistema.

---

## 🧠 Contexto

En BPMN una **Service Task** representa una actividad que realiza el sistema sin intervención humana.

Este tipo de tarea suele utilizarse para:

* ejecutar lógica de negocio
* llamar a APIs
* realizar cálculos
* integrar sistemas

En este ejercicio añadiremos una **Service Task** al proceso.

---

# Abrir el modelo del proceso

Abre **model/approval-process.bpmn** en **Camunda Modeler** (File → Open y navega a la carpeta model del repo) o ábrelo desde el explorador de VS Code si lo editas ahí.

---

# Insertar una Service Task

El proceso tiene ahora **Inicio → Fin**. Vamos a meter una tarea en medio. En la **paleta de la izquierda** toma **Task** (rectángulo con bordes redondeados) y **arrástrala** al canvas entre el evento de inicio y el de fin. Conecta con **Sequence Flow**: Inicio → Task → Fin.

---

# Convertir la tarea en Service Task

**Haz clic** en la tarea que acabas de crear. En el **panel de propiedades a la derecha** (o en un menú contextual al hacer clic derecho sobre la tarea) busca el **tipo de tarea**. Cámbialo a **Service Task** (en algunas versiones aparece como icono o en una lista desplegable "Task type"). Así la tarea será ejecutada automáticamente por el sistema.

---

# Renombrar la tarea

Asignar el siguiente nombre a la tarea:

```
Validar solicitud
```

---

# Conectar el flujo del proceso

Asegurarse de que el flujo queda de la siguiente forma:

```
Inicio → Validar solicitud → Fin
```

---

# Guardar el modelo

Guardar el archivo:

```
model/approval-process.bpmn
```

---

# Verificar el modelo

El diagrama BPMN debería contener:

* un evento de inicio
* una Service Task
* un evento de fin

Representando el flujo:

```
Inicio
   │
   ▼
Validar solicitud
   │
   ▼
Fin
```

---

# Qué significa esta tarea

La **Service Task** representa una actividad automática.

En laboratorios posteriores se implementará la lógica de esta tarea mediante **código Java**.

---

# Comprobación

El ejercicio se considera completado cuando:

* el modelo contiene una **Service Task**
* la tarea se llama **Validar solicitud**
* el flujo del proceso conecta inicio, tarea y fin
* el archivo BPMN se guarda correctamente.
