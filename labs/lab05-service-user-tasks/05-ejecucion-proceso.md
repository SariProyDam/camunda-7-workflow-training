# Ejecución del proceso

## 🎯 Objetivo

Iniciar una instancia del proceso y recorrer todo su flujo para verificar que:

* se ejecuta la **Service Task**
* se crea la **User Task**
* el proceso finaliza correctamente

---

## 🧠 Contexto

Hasta este punto del laboratorio ya se han configurado:

* una **Service Task** implementada con `JavaDelegate`
* una **User Task** asignada a un usuario o grupo

Ahora vamos a ejecutar el proceso completo para comprobar cómo el motor Camunda gestiona cada paso.

---

# Arrancar la aplicación

Abre una **terminal**. Desde la **raíz del repositorio** ejecuta `cd backend` y luego arranca la aplicación:

```bash
mvn spring-boot:run
```

Esperar a que el servidor arranque correctamente.

---

# Iniciar una instancia del proceso

El proceso se inicia desde el código Java mediante:

```java
runtimeService.startProcessInstanceByKey("approval-process");
```

Este método crea una **instancia del proceso** dentro del motor Camunda.

Cuando la aplicación arranca, se ejecutará este código y se iniciará el proceso.

---

# Verificar la ejecución de la Service Task

Durante la ejecución del proceso se ejecutará la clase:

```
ValidarSolicitudDelegate
```

En la consola debería aparecer el mensaje:

```
Ejecutando validación automática de la solicitud
```

Esto indica que el motor ha ejecutado la **Service Task**.

---

# Verificar la User Task en Tasklist

Abre el **navegador** y ve a **http://localhost:8081/camunda/app/tasklist** (usa el puerto que indique tu aplicación). Inicia sesión con el usuario que tenga la tarea asignada (por ejemplo **demo**).

En la lista de tareas debería aparecer:

```
Aprobar solicitud
```

---

# Completar la tarea

Seleccionar la tarea.

Presionar:

```
Complete
```

Esto permitirá que el proceso continúe hasta el evento de fin.

---

# Verificar el proceso en Cockpit

Abrir:

```
http://localhost:8081/camunda
```

Ir a **Cockpit** y abrir el proceso:

```
approval-process
```

Dentro del proceso se podrán observar:

* instancias activas
* instancias finalizadas
* historial del proceso

---

# Flujo completo del proceso

La ejecución del proceso sigue el siguiente flujo:

```
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

* la aplicación arranca correctamente
* la Service Task se ejecuta
* la User Task aparece en Tasklist
* la tarea se completa y el proceso finaliza.
