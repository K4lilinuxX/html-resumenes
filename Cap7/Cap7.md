**Almacenamiento local y HTML5**.  

* En resumen entendi que las apps nativas siempre han tenido ventaja porque el sistema operativo les permite guardar datos localmente (configuraciones, estado, bases de datos, etc.).  
* Las apps web antes de HTML5 estaban muy limitadas y básicamente solo tenían cookies, que son malas porque:  
   * Se envían en cada petición HTTP (hacen lenta la web).
   * Mandan datos al servidor (riesgo de seguridad si no hay SSL).
   * Solo permiten ~4 KB, casi inútil.  

Lo que se necesitaba era:  
* Mucho almacenamiento.  
* En el cliente (navegador).  
* Que persista aunque recargues la página.  
* Que NO se envíe al servidor.  

**Intentos antes de HTML5 (hackeos)**.  

Antes de HTML5 se intentaron varias soluciones, pero todas tenían problemas:  
1. Internet Explorer – userData.  
   * Permitía hasta 64 KB por dominio.
   * Solo funcionaba en IE.
   * Sin permisos ni opción de ampliar espacio.  
2. Flash – Local Shared Objects (cookies Flash).  
   * Hasta 100 KB por dominio.
   * Se podía ampliar con permiso del usuario.
   * Dependía de Flash (plugin externo).
   * Se usó con JavaScript vía herramientas como dojox.storage.  
3. Google Gears (2007).  
   * Usaba SQLite, una base de datos real.
   * Permitía almacenamiento casi ilimitado.
   * Requería instalar un plugin.
   * Luego fue abandonado.
4. dojox.storage.  
   * Intentaba unificar todas estas soluciones.
   * Detectaba Flash, Gears, AIR, etc.
   * Aun así, todo era inconsistente y dependía de plugins.  

**El problema y la solución**.  
* Todas las soluciones antiguas:
   * Eran específicas de un navegador
   * Dependían de plugins
   * Tenían límites y APIs diferentes.

* HTML5 vino a solucionar esto:
   * Una API estándar
   * Nativa en los navegadores
   * Sin plugins
   * Consistente entre Chrome, Firefox, Safari, etc.  

**¿Qué es el almacenamiento HTML5?**.  
* Se llama oficialmente Web Storage (también conocido como localStorage o DOM Storage).
* Permite a las páginas web guardar datos localmente en el navegador usando pares clave/valor.
* Los datos:
   * Persisten aunque cierres la pestaña o el navegador
   * NO se envían al servidor (a diferencia de las cookies)
   * No necesita plugins (es nativo del navegador).  

**Soporte en navegadores**.  
* Funciona en casi todos los navegadores modernos:  
   * IE 8+
   * Firefox 3.5+
   * Chrome 4+
   * Safari 4+
   * Opera 10.5+
   * iPhone y Android desde 2.0.  

Osea: sí se puede usar en producción sin miedo.  

**Cómo detectar si el navegador lo soporta**.  

* Se accede con `window.localStorage`.
* Puedes:
   * Detectarlo manualmente con JavaScript
   * O usar Modernizr, que lo hace más fácil y limpio.  

**Cómo funciona (uso básico)**.  
* Es un sistema de clave → valor
* La clave siempre es string
* El valor puede parecer número, booleano, etc., pero se guarda como string
   * Si guardas números → luego debes usar `parseInt()` o `parseFloat()`.  

**Operaciones principales:**
* Guardar: `setItem(key, value)`
* Obtener: `getItem(key)`
* Borrar una clave: `removeItem(key)`
* Borrar todo: `clear()`.  

**También puedes usarlo como si fuera un objeto:**.  
```js
localStorage["edad"] = 20;
``` 
**Recorrer el almacenamiento**.  
* `length` → cuántos datos hay
* `key(index)` → nombre de la clave según su posición.  

**Detectar cambios (storage event)**.  
* Existe un evento storage que se dispara cuando:
   * Se agrega
   * Se modifica
   * Se elimina un dato
* Sirve para:
   * Sincronizar pestañas
   * Reaccionar a cambios automáticamente.  

**HTML5 Storage en acción**.  
* Problema: si cierras el navegador, pierdes el progreso del juego.
* Solución: usar HTML5 Storage (localStorage) para guardar el estado del juego en el navegador.  

**¿Qué se guarda?**.  
Cada vez que el jugador hace un movimiento, se guarda:  
* Si hay una partida en curso (booleano)
* Posición (fila y columna) de cada pieza
* Qué pieza está seleccionada
* Si esa pieza ya se movió
* Número total de movimientos
Todo esto se guarda con pares clave/valor en `localStorage`.  

* Al cargar la página, en vez de empezar un juego nuevo:
   * Se llama a resumeGame()
   * Se revisa si hay datos guardados
   * Si existen, se reconstruye el estado completo del juego.  

**HTML5 Storage (localStorage / Web Storage)**.  
* Especificaciones oficiales
* Documentación de:
   * Microsoft (MSDN)
   * Mozilla (MDN)
   * Opera
   * IBM DeveloperWorks
* Sirve si quieres:
   * Entender bien cómo funciona
   * Ver ejemplos reales
   * Usarlo en web y móvil.  

**Antes de HTML5 (hacks viejos)**.  
* userData de Internet Explorer
* dojox.storage y Dojo Offline
* Trabajo de Brad Neuberg
* Todo esto es histórico:
* Ya no se usa
* Solo sirve para entender por qué HTML5 fue necesario.  

**Web SQL Database**.  
* Especificación y demos
* persistence.js (ORM sobre Web SQL)
* Importante:
* Web SQL está abandonado
* No es recomendable para proyectos nuevos
* Solo vale la pena leerlo por contexto histórico.  

**IndexedDB**.  
* Especificación oficial
* Artículos sobre su diseño
* Tutoriales tempranos (Firefox 4).  

**Cierre del capítulo (idea principal)**.  
* Este capítulo explica:
* Pasado: hacks, plugins y soluciones rotas
* Presente: HTML5 Storage (simple, estándar, usable)
* Futuro: IndexedDB (potente, escalable, serio)