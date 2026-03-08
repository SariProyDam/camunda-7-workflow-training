# Crear un JavaDelegate

## 🎯 Objetivo

Implementar la lógica de la **Service Task** creando una clase Java que será ejecutada por el motor Camunda.

---

## 🧠 Contexto

En el laboratorio anterior se creó una **Service Task** llamada:

```
Validar solicitud
```

Las Service Tasks representan actividades automáticas ejecutadas por el sistema.

En Camunda estas tareas suelen implementarse mediante una clase Java que implementa la interfaz:

```
JavaDelegate
```

Cuando el proceso alcance esta tarea, el motor ejecutará el código de esa clase.

---

# Crear el paquete de delegates

En el **explorador de archivos** de VS Code, entra en **backend** → **src** → **main** → **java**. Ahí verás los paquetes existentes (por ejemplo `com.example.workflow`). **Clic derecho** en el paquete raíz (por ejemplo `workflow`) → **New Folder** y crea **delegate** (o si tu proyecto usa otra estructura, crea la carpeta que corresponda al paquete `com.example.workflow.delegate`: por ejemplo las carpetas `com/example/workflow/delegate` dentro de **java**).

---

# Crear la clase Java

Dentro de la carpeta **delegate** (o **workflow/delegate** según tu estructura), **clic derecho** → **New File** y crea **ValidarSolicitudDelegate.java**. La ruta debe quedar algo como **backend/src/main/java/com/example/workflow/delegate/ValidarSolicitudDelegate.java** (ajusta `com.example.workflow` al paquete real de tu proyecto).

---

# Implementar la interfaz JavaDelegate

Añadir el siguiente código:

```java
package com.example.workflow.delegate;

import org.camunda.bpm.engine.delegate.DelegateExecution;
import org.camunda.bpm.engine.delegate.JavaDelegate;
import org.springframework.stereotype.Component;

@Component
public class ValidarSolicitudDelegate implements JavaDelegate {

    @Override
    public void execute(DelegateExecution execution) {

        System.out.println("Ejecutando validación automática de la solicitud");

    }
}
```

---

# Qué hace esta clase

La clase implementa la interfaz:

```
JavaDelegate
```

Esto permite que el motor Camunda ejecute el método:

```
execute()
```

cuando el proceso llegue a la **Service Task**.

En este ejemplo la lógica es simple y solo imprime un mensaje en consola.

---

# Compilar el proyecto

Abre una **terminal**. Desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Compilar el proyecto:

```bash
mvn clean package
```

---

# Verificar que el proyecto compila

Si todo es correcto, Maven mostrará al final:

```
BUILD SUCCESS
```

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea la clase `ValidarSolicitudDelegate`
* la clase implementa `JavaDelegate`
* el proyecto compila correctamente con Maven.
