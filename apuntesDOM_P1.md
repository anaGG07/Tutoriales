# **RESUMEN DOM EN JAVASCRIPT** 📜



### **&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; PRIMERA PARTE:** Acceso al DOM 🔍

<br>

## **Descripción básica**

### Es una representación estructurada de una página web, creada por el navegador cuando carga un documento HTML.
> #### El DOM es como un "árbol" donde cada elemento HTML (párrafos, imgágenes, enlaces...etc), es una "rama" o "nodo".

### **Ejemplo:**

```html
<button id="miBoton">Haz clic aquí</button>

<button> -> Es el nodo.
id="miBoton" -> Es el atributo, que en este caso, permite identificar al nodo.
```
<br>

## **Objetos principales**

### Para interactuar con la página web, el DOM cuenta con dos objetos principales:

### ``Window``
- Se puede definir como la "ventana" completa que incluye todo lo que se ve (y lo que no).
- Contiene otros elementos como métodos, propiedades, temporizadores...etc.

### ``Document``
- Se puede definir como el "papel" donde está escrito el contenido de la página, dentro de la "ventana" `(window)`
- Representa en sí el árbol de elementos, donde cada elemento es un "nodo".


### **Ejemplo:**

```javascript
Mostrar una alerta en el navegador es tarea de window
window.alert("Hola!");

Cambiar el texto de un título en la página, es del document
document.getElementById("miTitulo").innerText = "Nuevo texto";

```
<br>

## **Acceso a elementos del DOM**

### Métodos básicos para acceder a los elementos del DOM

### `document.getElementById("nombreId")`
- Busca un elemento por su ID único (nombreId).

  ### Ejemplo:

  ```javascript
  <h1 id="titulo">Hola, Mundo!</h1>

  const titulo = document.getElementById("titulo");

  Ahora la variable "titulo", se convierte en un objeto que apunta al elemento entero "<h1>", y se puede manipular con JavaScript.
  ```

<br>

### `document.getElementByClassName("nombreClase")`
- Busca todos los elementos que tienen una clase específica (nombreClase).
- Devuelve un `HTMLCollection`, similar a una lista. Se actualiza automáticamente.
  ### Ejemplo:

  ```javascript
  <p class="texto">Primer párrafo</p>
  <p class="texto">Segundo párrafo</p>

  const textos = document.getElementsByClassName("texto");
  ```


  Ahora la variable `textos`, se convierte en un `HTMLCollection`.
  Para acceder a cada elemento, se puede indexar como un array, `textos[0] -> "Primer párrafo"`.

  ```javascript
  Para recorrerlo, se puede convertir en array:

  const elementosArray = Array.from(elementos);

  elementosArray.forEach((elemento) => {
  console.log(elemento.innerText);
  });
  ```
<br>

### `document.getElementsByTagName("etiqueta")`
- Busca todos los elementos de un ***tipo*** de etiqueta HTML (`<div>`, `<p>`, `<button>`...etc)
- Devuelve una colección, `(HTMLCollection)`, de todos los elementos que coinciden con el nombre de la etiqueta.
- Se interactúa de la misma forma que con `getElementByClassName`

  ### Ejemplo:

  ```javascript
  <div> 1 </div>
  <div> 2 </div>
  <div> 3 </div>

  const divs = document.getElementsByTagName("div");
  divs[1]; // Accede al contenido del segundo <div>
  ```

<br>

### `document.querySelector("selector")`
- Busca el ***primer*** elemento que coincida con un selector CSS (como #id, .clase o etiqueta).
- Si no encuentra el elemento, devuelve `null`.
- Permite combinaciones de selectores.
  
  ### Ejemplo:

  ```javascript
  <p class="parrafo">Primer párrafo</p>
  <div class="parrafo">Segundo párrafo</div>

  const seleccion = document.querySelector(".parrafo");
  seleccion -> Apunta a <p class="parrafo">, ya que es el primer elemento que coincide.

  const seleccionCompleja = document.querySelector("div.parrafo");
  seleccionCompleja -> Ahora apunta a <div class="parrafo">, ya que es más específica.
  ```

  <br>

### `document.querySelectorAll("selector")`
- Encuentra ***todos*** los elementos que coincidan con un selector CSS.
- Devuelve una lista `(NodeList)` de todos los elementos que coinciden.

  ### Ejemplo:

  ```javascript
  <span class="resaltado">Texto 1</span>
  <span class="resaltado">Texto 2</span>
  <p class="resaltado">Parrafo 1</p>

  const resaltados = document.querySelectorAll(".resaltado");

  resaltados.forEach((resaltado) => {
  resaltado; // mostrará "Texto 1", "Texto 2" y "Parrafo 1"
  });

  const resaltadoEspecifico = document.querySelectorAll("p.resaltado");
  resaltadoEspecifico; // mostrará "Parrafo 1"
  ```

<br>

> [!NOTE] 
>  ### Diferencia entre `querySelectorAll` y `getElementsByClassName`
>  - `querySelectorAll` devuelve una `NodeList`, que permite usar métodos de array como `.forEach()` directamente.
>  - `getElementsByClassName` y `getElementsByTagName` devuelven una `HTMLCollection`, que debe convertirse a un array para usar métodos de array.
