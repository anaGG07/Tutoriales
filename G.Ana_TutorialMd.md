# Tutorial de Markdown

Markdown es un lenguaje de marcado ligero y sencillo que permite crear contenido formateado en texto plano. Se utiliza comúnmente en documentos README de proyectos de GitHub, blogs y otras plataformas que requieren una sintaxis simple.

---

## Estilos de texto

### Cursiva

Para aplicar **cursiva**, envuelve el texto con asteriscos o guiones bajos (`*` o `_`):

```markdown
*Texto en cursiva*
_texto en cursiva_
```

*Texto en cursiva*

---

### Negrita
Para aplicar negrita, utiliza dos asteriscos o guiones bajos (** o __):

```markdown
**Texto en negrita**
__Texto en negrita__
```
__Texto en negrita__

---

### Tachado
Para aplicar tachado, utiliza dobles virgulillas (~~):

```markdown
~~Texto tachado~~
```
~~Texto tachado~~

---

### Separadores

Para crear un separador o línea horizontal, utiliza tres o más guiones (---) o asteriscos (***):

```markdown
---
***
```
---

### Carácter de escape

Si necesitas usar caracteres especiales sin que se interpreten, usa el carácter de escape (\). Por ejemplo, para mostrar un asterisco:

```markdown
\*Escape de asterisco*
```
---

### Citas
Para crear una cita o blockquote, usa el símbolo mayor que (>):

```markdown
> Esto es una cita
```
> Esto es una cita

---

## Enlaces
### Enlace básico

Para crear un enlace, usa corchetes para el texto del enlace y paréntesis para la URL:

```markdown
[Texto del enlace](https://www.example.com)
```

[Texto del enlace](https://www.example.com)

### Enlace con título
Puedes agregar un title opcional que aparece al pasar el cursor sobre el enlace:

```markdown
[Enlace con título](https://www.example.com "Descripción del enlace")
```
[Enlace con título](https://www.example.com "Descripción del enlace")

---

## Listas
### Listas desordenadas
Para listas desordenadas, utiliza asteriscos (*), guiones (-) o signos más (+):

```markdown
* item 1
  * item 1.1
  * item 1.2
    * item 1.2.1
* item 2
* item 3
```

* item 1
  * item 1.1
  * item 1.2
    * item 1.2.1
* item 2
* item 3

### Listas ordenadas
Para listas ordenadas, usa números seguidos de un punto (1.):

```markdown
1. item 1
2. item 2
3. item 3
```
1. item 1
2. item 2
3. item 3

---
## Código
### Código en línea
Para resaltar código en una línea, usa comillas invertidas (```):

```markdown
`Esto es código en línea`
```
`Esto es código en línea`

### Bloques de código
Para agregar bloques de código, usa tres comillas invertidas (```).

Puedes especificar el lenguaje de programación después de las comillas invertidas para aplicar resaltado de sintaxis::

```markdown
```java
public class Persona {
    protected int edad;
}
\```
```

```java
public class Persona {
    protected int edad;
}
```
---

### Imágenes

Para insertar una imagen, usa un formato similar al de los enlaces, pero con un signo de exclamación al inicio (`!`):

```markdown
![Texto alternativo](https://example.com/logo.jpg)
```
![Logo Youtube](https://brandemia.org/sites/default/files/inline/images/logo_youtube.jpg)

---

### Tablas
Puedes crear tablas usando tuberías (|) y guiones (-) para separar las celdas y encabezados:
```markdown
| Nombre | Edad |
|--------|------|
| Jorge  | 23   |
```
| Nombre | Edad |
|--------|------|
| Jorge  | 23   |
---

### Listas de tareas
Para crear una lista de tareas con casillas de verificación, usa corchetes ([ ] para pendientes, [x] para completadas):

```markdown
* [x] Tarea 1
* [ ] Tarea 2
* [x] Tarea 3
```
* [x] Tarea 1
* [ ] Tarea 2
* [x] Tarea 3

> ¡Y eso es todo! Con esta guía puedes empezar a crear contenido elegante y estructurado con Markdown.