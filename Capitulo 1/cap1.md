Lo que entendí es que el texto explica cómo nació HTML5 y por qué hacer estándares web es complicado. Al igual que un desarrollador de Mozilla dice que:

**1. La tensión al crear estándares**

1° Si los navegadores implementan cosas antes de que el estándar esté terminado, la gente depende de esas funciones y eso limita el estándar. 2° Si el estándar se termina antes de que existan implementaciones, falta retroalimentación real.

**2. Tipos MIME (base técnica importante)**

Ahora cada vez que visitas una web, el servidor envia un encabezado como:

```HTML
Content-Type: text/html
```

Esto le dice al navegador qué tipo de archivo es (HTML, imagen, CSS, JS, etc.).
La web funciona gracias a estos tipos MIME. Aunque hoy parece normal, en 1993 ni siquiera existía ese encabezado, así que había confusión y errores que aún arrastramos.

**3. ¿De dónde salió la etiqueta `<img>`?**

También me sorprendió que la etiqueta `<img>` en 1993 Marc Andreessen (creador del navegador Mosaic y luego Netscape) propuso por primera vez:}

```HTML
<img src="imagen.xbm">
```
1. Al inicio, solo querían mostrar imágenes simples.
2. No existía aún MIME para imágenes.
3. Otros desarrolladores propusieron alternativas como `<icon>`, `<include>`,etc.
4. Hubo debates sobre cómo incrustar imágenes, audio, multimedia, etc.

Finalmente gano `<img>`porque era simple y ya funcionaba en Mosaic.

**4. Muchos intentos y prototipos**

Al igual me sorprendió que antes del W3C hubo muchos intentos o experimentos

1. Propuestas como `<include>`, `<icon>`, `<figure>`, etc.
2. Ideas para multimedia antes de `<video>` y `<audio>`.
3. Intentos de incrustar documentos completos dentro de otros.
4. Discusiones sobre si deberían usar MIME para todo.

Casi ninguna de esas ideas se implemento, pero sentaron las bases.

**5. Evolución del HTML**

Los estándares fueron avanzando asi:

1. HTML+ (no llegó)
2. HTML 2.0 (formalizó lo ya usado)
3. HTML 3.0 (muy ambicioso pero no implementado)
4. HTML 3.2 (otro retro-estándar)
5. HTML 4.0
6. Luego XHTML…
7. Y finalmente HTML5, creado por reaccionar a todos esos problemas.