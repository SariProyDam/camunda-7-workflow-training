# Establecer variables desde Java

## 🎯 Objetivo

Iniciar una instancia del proceso pasando **variables iniciales desde código Java**.

---

## 🧠 Contexto

Las variables de proceso pueden crearse de varias formas:

* desde **Java**
* desde **formularios**
* desde **Tasklist**
* desde **REST API**

En este ejercicio se iniciará el proceso pasando variables desde el código que arranca la instancia.

Esto permite enviar **datos de negocio al proceso** desde el inicio.

---

# Abrir la clase que inicia el proceso

En el **explorador** de VS Code entra en **backend** → **src** → **main** → **java** y abre la clase principal de la aplicación (por ejemplo **WorkflowAppApplication.java**; usa **Ctrl+P** y escribe el nombre si no la ves). Busca el código donde se inicia el proceso:

```java
runtimeService.startProcessInstanceByKey("approval-process");
```

---

# Crear un mapa de variables

Modificar el código para crear variables antes de iniciar el proceso.

Añadir un mapa de variables:

```java id="a9z3hk"
Map<String, Object> variables = new HashMap<>();

variables.put("solicitante", "juan");
variables.put("importe", 5000);
variables.put("tipoSolicitud", "compra");
```

---

# Iniciar el proceso con variables

Modificar la llamada al motor para enviar las variables.

Actualizar el código:

```java id="d8k1qa"
runtimeService.startProcessInstanceByKey("approval-process", variables);
```

---

# Código completo de ejemplo

El método quedará similar a:

```java id="p6v4wd"
@Bean
public CommandLineRunner startProcess(RuntimeService runtimeService) {
    return args -> {

        Map<String, Object> variables = new HashMap<>();

        variables.put("solicitante", "juan");
        variables.put("importe", 5000);
        variables.put("tipoSolicitud", "compra");

        runtimeService.startProcessInstanceByKey("approval-process", variables);

    };
}
```

---

# Compilar el proyecto

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Compilar el proyecto:

```bash
mvn clean package
```

---

# Ejecutar la aplicación

Arrancar la aplicación:

```bash
mvn spring-boot:run
```

Esto iniciará una instancia del proceso con variables.

---

# Verificar las variables en Cockpit

Abrir:

```
http://localhost:8081/camunda
```

Ir a **Cockpit**.

En Cockpit, en la lista de procesos **haz clic** en **approval-process**. Abre una instancia de la lista (si hay varias). En la vista de detalle, en el **menú o las pestañas** entra en la sección:

```
Variables
```

Deberían aparecer las variables:

```
solicitante
importe
tipoSolicitud
estadoSolicitud
```

---

# Qué ha ocurrido

El proceso se ha iniciado con variables iniciales.

El flujo sería:

```
Aplicación Java
      │
      ▼
runtimeService.startProcessInstanceByKey(...)
      │
      ▼
variables enviadas al proceso
      │
      ▼
variables disponibles en todo el workflow
```

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea un mapa de variables
* el proceso se inicia con variables
* las variables aparecen en **Camunda Cockpit** dentro de la instancia del proceso.
