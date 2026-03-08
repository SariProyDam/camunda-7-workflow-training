# Añadir una User Task

## 🎯 Objetivo

Modificar el modelo BPMN para añadir una **User Task**, que representa una tarea que debe ser realizada por una persona.

---

## 🧠 Contexto

En BPMN una **User Task** representa una actividad que requiere intervención humana.

Cuando un proceso alcanza una **User Task**, el motor Camunda:

1. crea una tarea
2. la asigna a un usuario o grupo
3. espera a que la tarea sea completada

Estas tareas se gestionan desde la aplicación **Camunda Tasklist**.

---

# Abrir el modelo del proceso

Abre **model/approval-process.bpmn** en **Camunda Modeler** (File → Open, carpeta model del repo).

---

# Añadir una nueva tarea

El flujo actual es **Inicio → Validar solicitud → Fin**. Añade una tarea humana antes del fin: en la **paleta de la izquierda** toma **Task** y **arrástrala** entre **Validar solicitud** y **Fin**. Conecta con **Sequence Flow** para que quede: Validar solicitud → nueva tarea → Fin.

---

# Convertir la tarea en User Task

**Haz clic** en la tarea que acabas de añadir. En el **panel de propiedades a la derecha** (o clic derecho → tipo de tarea) cambia el tipo a **User Task**. Así la tarea será atendida por una persona desde Tasklist.

---

# Renombrar la tarea

Asignar el nombre:

```
Aprobar solicitud
```

---

# Conectar el flujo del proceso

El proceso debería quedar con el siguiente flujo:

```
Inicio → Validar solicitud → Aprobar solicitud → Fin
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

* un **Start Event**
* una **Service Task**
* una **User Task**
* un **End Event**

Representando el flujo:

```
Inicio
   │
   ▼
Validar solicitud
   │
   ▼
Aprobar solicitud
   │
   ▼
Fin
```

---

# Qué ocurrirá durante la ejecución

Cuando el proceso llegue a la **User Task**:

1. el motor creará una tarea
2. la tarea aparecerá en **Tasklist**
3. un usuario podrá completarla
4. el proceso continuará hasta el evento de fin

---

# Comprobación

El ejercicio se considera completado cuando:

* el modelo contiene una **User Task**
* la tarea se llama **Aprobar solicitud**
* el flujo conecta correctamente todas las actividades
* el archivo BPMN se guarda correctamente.
