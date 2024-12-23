# **RESUMEN DOM EN JAVASCRIPT** 📜



### **&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; SEGUNDA PARTE:** Manipulación del DOM ✏️

<br>

## **Modificar el contenido de los elementos**

### Existen propiedades que permiten acceder y modificar el texto y el HTML de un elemento seleccionado.

### ``innerText:``
 -  ### Define o recupera el ***texto visible*** de un elemento, respetando el estilo CSS que tenga definido. 
  
    ### **Ejemplo de asignación:**

    ```JavaScript
    <div id="textoVisible"></div>

    const textoDiv = document.getElementById("textoVisible");
    textoDiv.innerText = "Este es el texto visible";
    // Solo permite texto, si se intenta introducir una etiqueta <p></p>, se imprime tal cual.
    ```

    ### **Resultado:**

    ```JavaScript
    <div id="textoVisible">
    Este es el texto visible
    </div>
    ```

    ### **Ejemplo de obtención:**
    
    ```JavaScript
    console.log(textoDiv.innerText);
    // Esto imprimiría -> "Este es el texto visible"
    ```
<br>

### ``innerHTML:``
 -  ### Define o recupera el contenido ***HTML completo*** de un elemento. JavaScript interpreta el valor como HTML y lo inserta completo dentro del elemento, lo que permite reemplazar o incluir texto, etiquetas, imagenes, listas...etc
  
    ### **Ejemplo básico:**
    
    ```JavaScript
    <p id="contenido"></p>
    
    Asignar un contenido:

    const contenidoP = document.getElementById("contenido");
    contenidoP.innerHTML = "Hola";

    contenidoP; // Esto contiene <p id="contenido">Hola</p>
    ```

    ### **Ejemplo de asignación HTML:**
    
    ```JavaScript
    <div id="contenido"></div>
    
    Asignar un contenido HTML:

    const contenidoDiv = document.getElementById("contenido");
    contenidoDiv.innerHTML = "<h1>Hola Mundo</h1><p>Este es un párrafo</p>";
    ```

    ### **Resultado:**

    ```JavaScript
    <div id="contenido">
      <h1>Hola Mundo</h1>
      <p>Este es un párrafo</p>
    </div>
    ```

    ### **Ejemplo de obtención:**
    
    ```JavaScript
    console.log(contenidoDiv.innerHTML);
    // Esto imprimiría -> <h1>Hola Mundo</h1><p>Este es un párrafo</p>
    ```

<br>

### ``textContent:``
 -  ### Define o recupera ***todo el texto*** de un elemento, incluyendo el texto que podría estar oculto por CSS. Es más rápido que `innerHTML` y captura todo el texto sin formato. 
  
    ### **Ejemplo de asignación:**
    
    ```JavaScript
    <div id="textoCompleto"></div>
    
    Asignar un contenido de texto completo:

    const textoCompletoDiv = document.getElementById("textoCompleto");
    textoCompletoDiv.textContent = "Este es el texto completo";

    ```

    ### **Resultado:**

    ```JavaScript
    <div id="textoCompleto">
    Este es el texto completo
    </div>

    ```

    ### **Ejemplo de obtención:**
    
    ```JavaScript
    console.log(textoCompletoDiv.textContent);
    // Esto imprimiría → "Este es el texto completo"
    ```

<br>

> [!NOTE] 
>  ### Diferencias entre `innerText` y `textContent`
>  - `innerText` Muestra solo el texto visible en la página. Respeta las propiedades CSS de visibilidad, excluyendo texto en elementos con `display: none;` o `visibility: hidden;`.
> 
>  - `textContent` Es más rápido que innerText, principalmente porque solo obtiene el texto, sin realizar ningún tipo de analisis de CSS.

<br>

## **Manipulación de clases**

### Cada elemento HTML puede tener clases para definir estilos específicos. Éstos se pueden manipular de la siguiente manera:

### ``className:``

 -  ### Propiedad que permite establecer o leer ***todas*** las clases de un elemento como una sola cadena de texto:
    - ### Añadir una clase
      
      ```JavaScript
      <div id="app">Este es un ejemplo</div>

      appDiv.className = "clase1";

      // El elemento ahora seria así
      <div id="app" class="clase1">Este es un ejemplo</div>
      ```

    - ### Añadir varias clases
        
      ```JavaScript
      <div id="app">Este es un ejemplo</div>

      appDiv.className = "clase1 clase2";
      
      // El elemento ahora seria así
      <div id="app" class="clase1 clase2">Este es un ejemplo</div>
      ```

    - ### Reemplazar una clase
        
      ```JavaScript
      <div id="app" class="clase1 clase2">Este es un ejemplo</div>


      const appDiv = document.getElementById("app"); // Recuperar el elemento
      appDiv.className = "nuevaClase"; // Reemplaza "clase1 clase2" por "nuevaClase"

      // El elemento ahora seria así
      <div id="app" class="nuevaClase">Este es un ejemplo</div>
      ```
    <br>

    > [!WARNING]
    > - ### Reemplazar una clase concreta:
    >   ### Se puede reemplazar una clase en concreto, utilizando el método `replace`. Pero puede causar problemas si la clase a reemplazar forma parte del nombre de otra clase.
    > 
    >
    >   ```JavaScript
    >   <div id="app" class="clase2 claseExtra clase2Extra">Ejemplo de clases</div>
    >   
    >   const appDiv = document.getElementById("app");
    >   appDiv.className = appDiv.className.replace("clase2", "nuevaClase2");
    > 
    >   // Resultado inesperado
    >   <div id="app" class="nuevaClase2 claseExtra nuevaClase2Extra">Ejemplo de clases</div>
    >   ```
    >   #### ***Es aconsejable utilizar `classList` para ello.***

<br>

### ``classList:``

 -  ### Propiedad que permite gestionar las clases CSS de un elemento. Permite:
    - ### Añadir una clase 
  
      #### ``classList.add("nombreClase"):``
      
      ```JavaScript
      <div id="app">Este es un ejemplo</div>

      const appDiv = document.getElementById("app"); // Se obteniene el elemento
      appDiv.classList.add("clase1"); // Añadir la clase "clase1" al elemento

      // El elemento ahora sería asi
      <div id="app" class="clase1">Este es un ejemplo</div>
      ```

    <br>

    -  ### Quitar una clase del elemento
    
       #### ``classList.remove("nombreClase"):``
      
       ```JavaScript
       <div id="app" class="clase1">Este es un ejemplo</div>

       const appDiv = document.getElementById("app"); // Se obteniene el elemento
       appDiv.classList.remove("clase1"); // Quita la clase "clase1" del elemento
       
       // El elemento ahora sería asi
       <div id="app">Este es un ejemplo</div>
       ```

    <br>

    -  ### Alternar una clase: la agrega si no está o la quita si ya está.
  
       #### ``classList.toggle("nombreClase"):``
      
       ```JavaScript
       <div id="app">Este es un ejemplo</div>

       const appDiv = document.getElementById("app"); // Se obteniene el elemento
       appDiv.classList.toggle("activo"); // Alternar la clase "activo" (añade porque no está)

       // El elemento ahora sería asi
       <div id="app" class="activo">Este es un ejemplo</div>

       appDiv.classList.toggle("activo"); // Si se vuelve a ejecutar, elimina la clase

       // El elemento vuelve a su estado original
       <div id="app">Este es un ejemplo</div>
       ```

<br>

## **Manipular atributos de los elementos**

### Los atributos son propiedades que se asignan a los elementos (``href``, ``src``, ``alt``, ``id``, ``class``...etc). Métodos principales para manipular atributos:

<br>

### ``setAttribute("nombreAtributo", "valor"):``
- ### Si el atributo introducido ya existe, actualiza el valor. Si no existe, lo crea y le asigna el valor especificado.

  ```JavaScript
  <a id="miEnlace" href="https://ejemplo.com">Visita mi página</a>

  const miEnlace = document.getElementById("miEnlace"); // Obtener el elemento

  miEnlace.setAttribute("href", "https://miSitioWeb.com"); // Actualiza el atributo "href" porque ya existe

  miEnlace.setAttribute("target", "_blank"); // Añade el atributo "target"

  // Resultado:
  <a id="miEnlace" href="https://miwebsite.com" target="_blank">Visita mi página</a>
  ```


<br>


### ``getAttribute("nombreAtributo"):``
- ### Si existe, recupera el valor del atributo especificado. Si no existe, devuelve null.

  ```JavaScript
  <a id="miEnlace" href="https://ejemplo.com">Visita mi página</a>

  const url = miEnlace.getAttribute("href"); // Obtiene el valor de "href"
  console.log(url); // Muestra: "https://ejemplo.com"

  const target = miEnlace.getAttribute("target");
  console.log(target); // Muestra: "null"
  ```

<br>

### ``removeAttribute("nombreAtributo"):``
- ### Borra completamente el atributo en el DOM, como si nunca hubiera existido.

  ```JavaScript
  <a id="miEnlace" href="https://ejemplo.com">Visita mi página</a>

  miEnlace.removeAttribute("target"); // Elimina el atributo "href"
  
  // Resultado
  <a id="miEnlace">Visita mi página</a>
  ```

<br>

>[!NOTE]
> ### Estos métodos, se pueden emplear en validaciones con ``if()``, para verificar si un atributo está presente o cumple un valor concreto.
>
> ```JavaScript
> const miBoton = document.getElementById("miBoton");
>
> // Añadir el atributo target solo si no existe, para evitar pisar el valor anterior
> if (!miBoton.getAttribute("target")) {
>    miBoton.setAttribute("target", "_blank");
> }
> ```
> 
> ### También se pueden emplear operadores de cortocircuito ` (&& y ||)` para ejecutar acciones o establecer valores alternativos.
>
> ```JavaScript
> // Si el atributo activo existe, se ejecuta setAttribute
> miBoton.getAttribute("activo") && miBoton.setAttribute("estado", "activo");
> ```