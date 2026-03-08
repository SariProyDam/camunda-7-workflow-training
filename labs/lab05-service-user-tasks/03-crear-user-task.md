# Crear una User Task

## 🎯 Objetivo

Configurar la **User Task** del proceso para que pueda ser gestionada desde **Camunda Tasklist**.

---

## 🧠 Contexto

En el modelo BPMN se añadió previamente una tarea humana llamada:

```id="5f3q4s"
Aprobar solicitud
```

Cuando el proceso alcanza una **User Task**, el motor Camunda:

1. crea una tarea
2. la asigna a un usuario o grupo
3. espera a que alguien complete la tarea

Estas tareas se gestionan desde la aplicación web:

```id="c6h34p"
/camunda/app/tasklist
```

Para que la tarea pueda aparecer correctamente en Tasklist es necesario configurar **quién puede realizarla**.

---

# Abrir el modelo BPMN

Abre **model/approval-process.bpmn** en **Camunda Modeler** (File → Open, carpeta model del repo).

---

# Seleccionar la User Task

En el diagrama, **haz clic** en la tarea **Aprobar solicitud**. En el **panel de propiedades a la derecha** verás las opciones de la User Task.

---

# Configurar el asignatario

En el panel de propiedades busca la sección **Assignment** (o "Asignación"). Ahí está el campo **Assignee** (asignatario). Escribe: **demo**.

Así la tarea se asignará al usuario **demo** (debe existir en Camunda; si usas demo/demo en application.properties, ese usuario suele estar creado).

---

# Guardar el modelo

Guardar los cambios:

```id="y7e2jq"
model/approval-process.bpmn
```

---

# Copiar el modelo al backend

Actualizar el modelo desplegado en el backend:

```bash id="j6g1oz"
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Reiniciar la aplicación

En la terminal, desde la raíz del repo: `cd backend`. Arranca la aplicación:

```bash id="w4n5lp"
mvn spring-boot:run
```

---

# Iniciar un proceso

Cuando el proceso se ejecute:

1. se ejecutará la **Service Task**
2. el proceso llegará a la **User Task**

En ese momento el motor creará una tarea para el usuario configurado.

---

# Verificar en Tasklist

Abre el **navegador** y ve a **http://localhost:8081/camunda/app/tasklist** (cambia 8081 por tu puerto si es otro). Inicia sesión con **demo** / **demo** (o el usuario que tengas configurado).

En la **lista de tareas** debería aparecer **Aprobar solicitud** una vez que hayas iniciado una instancia del proceso.

---

# Completar la tarea

Haz **clic** en la tarea en la lista. Se abrirá el detalle. Pulsa el botón **Complete** (o "Completar") para cerrar la tarea y que el proceso continúe hasta el fin.

Esto permitirá que el proceso continúe hasta el evento de fin.

---

# Flujo del proceso

El proceso ahora se ejecuta de la siguiente forma:

```id="f8s7b2"
Inicio
   │
   ▼
Validar solicitud (Service Task)
   │
   ▼
Aprobar solicitud (User Task)
   │
   ▼
Fin
```

---

# Comprobación

El ejercicio se considera completado cuando:

* la User Task tiene configurado el **assignee**
* la tarea aparece en **Tasklist**
* el usuario puede completar la tarea y finalizar el proceso.
