**¿Cómo hacer que una aplicación web funcione sin conexión a Internet?**.  
La página explica cómo hacer que una aplicación web funcione sin conexión a Internet usando una tecnología de HTML5 llamada Application Cache (AppCache).  
La idea central es:  
descargar y guardar los archivos de una web cuando hay Internet, para que después puedan usarse offline.    
**Concepto clave**.  
Una aplicación web offline:
* No se descarga cuando estás desconectado
* Se descarga antes, cuando tienes conexión
* Luego el navegador usa los archivos guardados localmente.  

Esto se logra con un archivo de manifiesto de caché (`.manifest`).  

**El archivo de manifiesto**.  
El manifiesto:  
* Es un archivo de texto
* Lista todos los recursos que la app necesita:
   * HTML
   * CSS
   * JavaScript
   * Imágenes, etc.  

Empieza siempre con:  
```objetivec
CACHE MANIFEST
```  

Y se conecta al HTML así:  
```html
<html manifest="archivo.manifest">
```  

**Secciones del manifiesto**.  
La página explica tres secciones importantes:  
**CACHE**.  
Archivos que:  
* Se descargan
* Se guardan
* Funcionan sin Internet.  

**NETWORK**.
* Nunca se guardan
* Requieren conexión (APIs, tracking, etc.).  

**FALLBACK**.  
Define qué mostrar:  
* Si un recurso no existe offline
* Por ejemplo, una página “sin conexión”.  
Esto permite apps grandes que:  
* Guardan páginas conforme el usuario las visita
* No necesitan listar todo desde el inicio.  

**Flujo de eventos**.  
El navegador maneja la caché con eventos como:  
* `checking`
* `downloading`
* `progress`
* `cached`
* `noupdate`
* `updateready`
* `error`.  

Estos eventos indican:  
* Si la app se está descargando
* Si ya está lista
* Si hubo errores
* Si hay una versión nueva.  

Ejemplo práctico.  
Se usa un juego (Halma) para mostrar que:
* Con solo un HTML y un JS
* Y un manifiesto bien hecho
* El juego puede funcionar 100% offline
* Guardando su estado con `localStorage`.  

**Conclusión importante**.  
* AppCache fue una tecnología clave en HTML5
* Hoy está obsoleta
* Fue reemplazada por Service Workers
* Pero entender AppCache ayuda mucho a comprender:
   * PWA
   * Apps offline modernas
   * Caché inteligente en el navegador