# Eventos de inicio y fin

## 🎯 Objetivo

Modificar el modelo BPMN para añadir **eventos de inicio y fin**, definiendo claramente dónde comienza y termina el proceso.

---

## 🧠 Contexto

En BPMN todo proceso debe tener al menos:

* un **evento de inicio**
* un **evento de fin**

Estos elementos definen el flujo básico de ejecución del proceso.

El motor Camunda inicia el proceso desde el **Start Event** y lo finaliza cuando alcanza un **End Event**.

---

# Abrir el modelo del proceso

Abre el archivo del paso anterior. En **Camunda Modeler**: menú **File** (arriba) → **Open** (o **Open File**). Navega hasta la carpeta **model** del repositorio y selecciona **approval-process.bpmn**. Se abrirá el diagrama. (También puedes abrirlo desde VS Code: en el explorador, **model/approval-process.bpmn**, y si quieres editarlo en Modeler, abre ese archivo con la aplicación Camunda Modeler.)

---

# Añadir evento de inicio

En la **paleta de la izquierda** (panel de herramientas) busca **Start Event** (círculo simple). **Arrástralo** al canvas y suéltalo donde quieras que empiece el flujo.

Asignar el nombre:

```
Inicio
```

Este evento representa el punto donde el proceso comienza.

---

# Añadir evento de fin

En la **paleta de la izquierda** busca **End Event** (círculo con borde grueso). Arrástralo al diagrama y colócalo donde deba terminar el proceso.

Asignar el nombre:

```
Fin
```

Este evento representa el final del proceso.

---

# Conectar los eventos

En la **paleta** selecciona **Sequence Flow** (la flecha/conector). Haz **clic** en el Start Event (Inicio) y **arrastra** hasta el End Event (Fin). O haz clic en el primero y luego en el segundo si tu versión lo permite. Debe quedar una flecha: **Inicio → Fin**.

Esto crea el flujo mínimo de un proceso BPMN.

---

# Guardar el modelo

Guardar los cambios en el archivo:

```
model/approval-process.bpmn
```

---

# Verificar el diagrama

El modelo debería representar un flujo similar a:

```
Inicio → Fin
```

Este es el **proceso BPMN más simple posible**.

---

# Qué ocurre en el motor

Cuando el motor ejecuta este proceso:

1. se inicia la instancia
2. se alcanza el evento de inicio
3. el flujo avanza directamente al evento de fin
4. el proceso termina

---

# Comprobación

El ejercicio se considera completado cuando:

* el modelo contiene un **Start Event**
* el modelo contiene un **End Event**
* ambos elementos están conectados
* el archivo BPMN se guarda correctamente.
