**¿Qué es una aplicación web fuera de línea (offline)?**.  

Una aplicación web offline es una web que puede seguir funcionando aunque no tengas Internet, porque descarga y guarda sus archivos cuando estás en línea y luego usa esas copias locales cuando te desconectas.  

Esto se logra con HTML5 usando algo llamado archivo de manifiesto de caché (cache manifest).  

**¿Cómo funciona?**.  
1. La web tiene un archivo de manifiesto, que es solo un archivo de texto.
2. Ese archivo contiene una lista de recursos que la app necesita:
   * HTML
   * CSS
   * JavaScript
   * Imágenes, etc.
3. El navegador:
   * Lee el manifiesto
   * Descarga esos archivos
   * Los guarda en caché local
4. Cuando no hay Internet, el navegador usa las versiones guardadas automáticamente.  

**¿Qué debe hacer el desarrollador?**.  

HTML5 solo te da la base:
   * Saber si estás online u offline
   * Detectar cuando cambia el estado de conexión.  

Pero:  
   * Guardar datos localmente
   * Sincronizar con el servidor cuando vuelve Internet
   * Eso ya es responsabilidad del desarrollador.  

**El archivo `cache.manifest`**.  

odas las páginas HTML deben apuntar al mismo manifiesto:  

```html
<html manifest="/cache.manifest">
```

El archivo debe empezar siempre con:  
```objetivec
CACHE MANIFEST
```  

Y debe servirse con el tipo:  

```pgsql
text/cache-manifest
``` 

**Secciones del manifiesto**.  

1. CACHE.  
Archivos que:  
   * Se descargan
   * Se guardan
   * Funcionan offline.  

Ejemplo:  

```bash
CACHE MANIFEST
/clock.css
/clock.js
/clock-face.jpg
```  

2. NETWORK.  
Archivos que:
* Nunca se guardan
* Solo funcionan con Internet.  

Ejemplo:  

```bash
NETWORK:
/tracking.cgi
```  

Útil para:  
* Scripts de tracking
* APIs
* Recursos dinámicos.  

3. FALLBACK.  

Define qué mostrar si un recurso no está disponible offline.  

Ejemplo:  

```bash
FALLBACK:
/ /offline.html
```  

Si visitas una página sin Internet y no está en caché, en lugar de error se muestra `offline.html`.  

4. El flujo de eventos en aplicaciones web offline (AppCache).  

Cuando una página web tiene un archivo de manifiesto de caché, el navegador sigue un flujo de eventos DOM usando el objeto:  

```js
window.applicationCache
```   

Nada es mágico: todo pasa mediante eventos.  

**`checking`**.  
* Se dispara siempre
* Ocurre apenas el navegador ve el atributo manifest
* No importa si ya visitaste antes la página o no.  

**Caso 1: el navegador nunca ha visto el manifiesto**.  

`checking`.  
`downloading` → empieza a bajar los recursos.  
`progress` → se dispara varias veces mientras descarga.  
`cached` → todo se guardó correctamente.  

**Caso 2: el navegador ya conoce el manifiesto**.  
Ahora el navegador se pregunta: ¿El manifiesto cambió?  

NO cambió.  
* Evento: `noupdate`
* Fin del proceso.  

SÍ cambió.  
* `downloading`
* varios `progress`
* `updateready`.  

OJO:
La nueva versión NO se usa automáticamente
Para activarla sin recargar:  

```js
window.applicationCache.swapCache()
```  

**Evento `error`**.  

Si algo falla, se dispara `error` y no te dice exactamente qué fue.  
Cosas que pueden causar error:  
* El manifiesto devuelve 404 o 410
* Un solo recurso del manifiesto falla al descargarse
* El manifiesto cambia durante la actualización
* Un archivo listado no se puede bajar.  

Si falla UN solo archivo, falla TODO.  

**Problema grande #1: depuración infernal**.  
* No sabes qué archivo falló
* Un error mínimo rompe toda la app offline
* Debuggear AppCache es dolor puro.  

Problema grande #2: el manifiesto NO se actualiza (y parece bug).  
El navegador revisa el manifiesto en 3 fases:  
Fase 1: caché HTTP.  
El navegador primero revisa:  
* `Cache-Control`
* `Expires`
* Si no ha expirado, ni siquiera pregunta al servidor.  

Fase 2: validación HTTP.  
* Si expiró, pregunta al servidor:
* Si no cambió → `304 Not Modified`
* Si cambió → `200 OK` + archivo nuevo.  

Fase 3: comparación interna
* Si el contenido del manifiesto es igual al anterior:
* NO se descargan los recursos otra vez.  

**Construyendo una app web offline**.  

La idea es convertir el juego Halma en una aplicación que funcione sin Internet, usando AppCache.  

El juego es perfecto para esto porque:
* Solo usa HTML
* Un solo archivo JavaScript
* No tiene imágenes (todo se dibuja con canvas)
* El CSS está embebido en el HTML
* Ya guarda su estado con localStorage.  

**Paso 1: Crear el archivo de manifiesto**.  
El manifiesto solo necesita listar los archivos esenciales:  
```bash
CACHE MANIFEST
halma.html
../halma-localstorage.js
```  

**Estructura de archivos**.  
El proyecto queda así:  
```bash
/examples/
 ├─ localstorage-halma.html
 ├─ halma-localstorage.js
 └─ offline/
     ├─ halma.manifest
     └─ halma.html
```  

**Paso 2: Conectar el HTML al manifiesto**.  
En el archivo `halma.html` solo se agrega esto:  
```html
<html lang="en" manifest="halma.manifest">
```  

**¿Qué pasa ahora?**.  
La primera vez que el navegador carga la página:  
1. Detecta el `manifest`
2. Descarga el archivo `.manifest`
3. Descarga los recursos listados
4. Los guarda en la appcache.  

A partir de ahí:
* El juego funciona sin conexión
* El estado se conserva con localStorage
* Puedes cerrar, volver, desconectarte y seguir jugando.  

**Idea clave final**.  

Hacer una app offline puede ser sorprendentemente simple si:
* Controlas tus recursos
* Sabes exactamente qué archivos necesita tu app
En este caso:
* 1 HTML
* 1 JS
* 0 imágenes.  
= offline perfecto