
# GIT

- https://www.youtube.com/watch?v=jVPMTR0SJCw
- https://commitlint.js.org/#/reference-rules
- https://github.com/conventional-changelog/commitlint

Los commits semánticos son una especificación para dar significado a los mensajes de los commits haciéndolos mas legibles.  Se propone estandarizar los mensajes de los commit de tal manera que podamos identificar el tipo de cambio que se realiza, además de una breve descripción clara y concisa. Recordemos que los commits son el guión de la historia de nuestros proyectos.

El objetivo es evitar que se suban al repositorio commits sin sentido alguno, y que el historial de git quede ordenado, estructurado, limpio. 

El formato que se propone es el siguiente **type (scope?): description**, donde:

***type*** es el identificador

***scope*** es opcional y corresponde a una agrupación

***description**** es el mensaje claro y conciso del commit. 

***Ejemplo:***

```bash
type(scope?): description
feat: add title commit
^--^  ^------------^
|     +-> # Short description for changes.
+-------> # Type: chore, docs, feat, fix, refactor, style, or test.
```
## SIGNIFICADO DE LOS TIPOS

-   **feat**: Cuando un commit agrega una nueva característica a nuestra APP o es una evolución.
-   **fix**: Cuando el commit representa una corrección a una funcionalidad.
-   **docs**: Cuando añadamos o actualizamos la documentación al proyecto.
-   **style**: Cuando hay cambios de formato (guía de estilo). No se altera el código de producción.
-   **refactor**: Cuando se modifica el código de producción, por ejemplo renombrar una variable, simplificar un método, etc…
-   **test**: Cuando se añaden o modifican los tests unitarios.
-   **chore**: Para tareas rutinarias, por ejemplo se modifica el .gitignore etc… No se altera el código de producción.

## BUENAS PRÁCTICAS PARA ESCRIBIR COMMITS.

### 1. Usar el verbos en el titulo (Agregar, Cambiar, Arreglar, Eliminar, …)
Estamos tentados a escribir commit sin sentido pero cada commit es una instrucción para cambiar el estado del proyecto.

***Ejemplo***
```bash
git commit -m "muchos cambios" ❌
git commit -m "Verbo: mensaje" ✅
```
### 2. No uses punto final ni puntos suspensivos en el título del mensaje
El primer mensaje del commit es el título. Los títulos no se puntúan.

***Ejemplo***
```bash
git commit -m "Agregar nueva función de búsqueda." ❌
git commit -m "Solucionar un problema con la barra superior..." ❌
git commit -m "Cambiar el color del sistema predeterminado" ✅
```
### 3. Usar como máximo 50 carácteres para tu mensaje de commit
Si existen muchos cambios haz que el mensaje sea claro, directo y que realmente refleje los cambios que lleva.

### 4. Usar el cuerpo del commit
Si el primer mensaje del commit es el título, los siguientes serían el cuerpo.
Ahí puedes usar la puntuación y además describir qué hace el commit:

***Ejemplo***
```bash
git commit -m "Agregar resumen" -m "Este es un mensaje para agregar más contexto."✅
git commit -m "Agregar pruebas unitarias" -m "Este es un mensaje para agregar más contexto."✅
```

### 5. Usar commits semánticos
Cuando un proyecto crece, es necesario que existan ciertas reglas para que el historial sea legible o para poder hacer releases automáticos.

### 6. Aprovecha los mensajes

***Ejemplo***
```bash
❌ "Eliminar CSS no utilizado"
✅ "Eliminar estilos de botones no utilizados de la página de pagina1/pagina2"

❌ "Agregar nueva característica"
✅ "Agregar funcionalidad de búsqueda por ciudad para usuarios registrados"

❌ "Arreglar error"
✅ "Arreglar el flujo de autenticación agregando una redirección a la página de inicio"
```
### 7. Instalar extensión en Visual Studio Code
Conventional Commits
