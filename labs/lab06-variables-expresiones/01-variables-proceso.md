# Variables de proceso

## 🎯 Objetivo

Comprender cómo funcionan las **variables de proceso** creando y utilizando una variable dentro del flujo BPMN.

---

## 🧠 Contexto

Los procesos BPMN pueden almacenar información durante su ejecución mediante **variables de proceso**.

Estas variables permiten:

* compartir datos entre tareas
* tomar decisiones en el flujo
* almacenar información de negocio

Las variables viven dentro de la **instancia del proceso**.

Por ejemplo:

```id="3mqs8s"
importeSolicitud
usuario
resultadoValidacion
```

En este ejercicio crearemos una variable llamada:

```id="s7l1e3"
estadoSolicitud
```

---

# Abrir el JavaDelegate

En el **explorador** de VS Code entra en **backend** → **src** → **main** → **java** y localiza la clase **ValidarSolicitudDelegate.java** (suele estar en un paquete **delegate** dentro de workflow). Ábrela. O usa **Ctrl+P** y escribe `ValidarSolicitudDelegate`.

---

# Añadir una variable de proceso

Modificar el método `execute` para guardar una variable en el proceso.

Actualizar el código:

```java id="k2zj7x"
@Override
public void execute(DelegateExecution execution) {

    System.out.println("Ejecutando validación automática de la solicitud");

    execution.setVariable("estadoSolicitud", "VALIDADA");

}
```

---

# Qué hace este código

La instrucción:

```java id="q7y5bm"
execution.setVariable("estadoSolicitud", "VALIDADA");
```

crea una variable de proceso llamada:

```
estadoSolicitud
```

y le asigna el valor:

```
VALIDADA
```

Esta variable quedará disponible para el resto del proceso.

---

# Compilar el proyecto

Abre una **terminal**. Desde la **raíz del repositorio** ejecuta `cd backend` y luego:

Compilar el proyecto:

```bash id="1vkn0h"
mvn clean package
```

---

# Ejecutar la aplicación

Arrancar la aplicación:

```bash id="h7r3sk"
mvn spring-boot:run
```

Esto iniciará una instancia del proceso.

---

# Verificar la variable en Cockpit

Abrir:

```
http://localhost:8081/camunda
```

Ir a **Cockpit**.

En la lista, **haz clic** en el proceso **approval-process**. Abre una de las instancias (si hay varias). En el **menú o las pestañas** de la vista de detalle, entra en la sección:

```
Variables
```

Debería aparecer la variable:

```
estadoSolicitud = VALIDADA
```

---

# Qué ha ocurrido

Durante la ejecución del proceso:

```id="5j2xqa"
Service Task
      │
      ▼
JavaDelegate
      │
      ▼
execution.setVariable(...)
      │
      ▼
variable almacenada en el proceso
```

El motor guarda la variable en la base de datos del proceso.

---

# Comprobación

El ejercicio se considera completado cuando:

* se modifica el `JavaDelegate`
* se crea la variable `estadoSolicitud`
* la variable aparece en **Cockpit** dentro de la instancia del proceso.
