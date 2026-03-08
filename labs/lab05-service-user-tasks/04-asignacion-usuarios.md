# Asignación de usuarios

## 🎯 Objetivo

Configurar la **User Task** para que pueda ser asignada a un **grupo de usuarios**, permitiendo que cualquiera de los miembros del grupo pueda realizar la tarea.

---

## 🧠 Contexto

En el ejercicio anterior la tarea se asignó directamente a un usuario:

```id="e3n1a4"
Assignee = demo
```

Esto significa que **solo ese usuario puede completar la tarea**.

En muchos procesos reales las tareas no se asignan a una persona concreta sino a un **grupo de trabajo**.

Por ejemplo:

* revisores
* analistas
* administradores

En Camunda esto se configura mediante:

```id="r5q2ns"
Candidate Groups
```

---

# Abrir el modelo BPMN

Abre **model/approval-process.bpmn** en **Camunda Modeler** (File → Open, carpeta model del repo).

---

# Seleccionar la User Task

En el diagrama, **haz clic** en la tarea **Aprobar solicitud**. En el **panel de propiedades a la derecha** se mostrarán sus opciones.

---

# Eliminar el assignee

En el panel de propiedades, en la sección **Assignment**, localiza el campo **Assignee**. Borra el valor que tenga (por ejemplo "demo") y déjalo vacío.

---

# Configurar el grupo candidato

En la misma sección **Assignment** busca el campo **Candidate Groups** (grupos candidatos). Introduce: **managers** (o el nombre del grupo que tengas creado en Camunda).

Esto indica que cualquier usuario perteneciente al grupo **managers** podrá reclamar o completar la tarea.

---

# Guardar el modelo

Guardar el archivo:

```id="z2m4cn"
model/approval-process.bpmn
```

---

# Copiar el modelo al backend

Actualizar el modelo desplegado en el backend:

```bash id="a1v7yu"
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Reiniciar la aplicación

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Arrancar la aplicación:

```bash id="m4x2qn"
mvn spring-boot:run
```

---

# Verificar en Tasklist

Abrir:

```id="n5q8zr"
http://localhost:8081/camunda/app/tasklist
```

Iniciar sesión con el usuario:

```id="g2w7tx"
demo
```

Si el usuario pertenece al grupo **managers**, la tarea aparecerá disponible para ser reclamada.

---

# Reclamar la tarea

Seleccionar la tarea **Aprobar solicitud**.

Presionar:

```id="v8f3qh"
Claim
```

Esto asigna la tarea al usuario actual.

Después se podrá completar con:

```id="d1j5rp"
Complete
```

---

# Qué ocurre en el proceso

Cuando el proceso llega a la User Task:

1. el motor crea la tarea
2. la tarea queda disponible para el grupo
3. un usuario del grupo la reclama
4. el usuario completa la tarea

---

# Comprobación

El ejercicio se considera completado cuando:

* la User Task tiene configurado **Candidate Groups**
* la tarea aparece disponible en Tasklist
* un usuario puede reclamar y completar la tarea.
