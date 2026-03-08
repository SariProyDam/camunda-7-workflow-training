# Formularios de tareas

## 🎯 Objetivo

Añadir un **formulario simple** a la **User Task** para introducir información cuando el usuario complete la tarea.

---

## 🧠 Contexto

Las **User Tasks** pueden mostrar formularios para que el usuario introduzca datos.

Estos formularios permiten:

* recoger información del usuario
* actualizar variables del proceso
* tomar decisiones dentro del workflow

Camunda permite definir formularios directamente en el modelo BPMN.

---

# Abrir el modelo BPMN

Abrir el archivo:

```
model/approval-process.bpmn
```

Editar el modelo utilizando **Camunda Modeler**.

---

# Seleccionar la User Task

Seleccionar la tarea:

```
Aprobar solicitud
```

---

# Crear un formulario

En el panel de propiedades buscar la sección:

```
Forms
```

Seleccionar:

```
Camunda Forms
```

---

# Añadir un campo al formulario

Añadir un nuevo campo con los siguientes valores.

Id:

```
aprobada
```

Label:

```
Solicitud aprobada
```

Type:

```
boolean
```

Este campo permitirá indicar si la solicitud ha sido aprobada.

---

# Guardar el modelo

Guardar el archivo:

```
model/approval-process.bpmn
```

---

# Copiar el modelo al backend

Actualizar el modelo desplegado en el backend:

```bash
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Ejecutar la aplicación

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Arrancar la aplicación:

```bash
mvn spring-boot:run
```

---

# Abrir Tasklist

Abrir en el navegador:

```
http://localhost:8081/camunda/app/tasklist
```

Iniciar sesión con el usuario correspondiente.

---

# Abrir la tarea

Seleccionar la tarea:

```
Aprobar solicitud
```

Ahora debería aparecer el formulario configurado.

El formulario mostrará el campo:

```
Solicitud aprobada
```

---

# Completar la tarea

Seleccionar el valor del campo.

Presionar:

```
Complete
```

Esto guardará la variable del formulario dentro del proceso.

---

# Qué ha ocurrido

Cuando el usuario completa la tarea:

```
Formulario
     │
     ▼
Variable aprobada
     │
     ▼
Guardada en la instancia del proceso
```

La variable estará disponible para el resto del flujo BPMN.

---

# Comprobación

El ejercicio se considera completado cuando:

* la User Task tiene un formulario configurado
* el formulario aparece en Tasklist
* el campo `aprobada` se guarda como variable del proceso.
