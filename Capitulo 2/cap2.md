**1. No existe "soporte HTML5"**

Lo que entendi de la lectura es que HTML5 no es una sola cosa, sino muchas funciones individuales. Por eso no puedes detectar si un navegador soporta HTML5, sino funciones especificas como:
1. canvas
2. video
3. geolocalizacion
4. nuevos tipos de input, etc.

**2. ¿Cómo detectar soporte de una función HTML5?**

El navegador crea un DOM, donde cada elemento HTML es un objeto.  

Puedes detectar soporte inspeccionando si ciertas propiedades o métodos existen.  

Las 4 tecnicas principales son:  
1. Revisar si existe una propiedad en un objeto global  
Ejemplo: geolocalizacion  
```js
if ('geolocation' in navigator) {
}
```  
2. Crear un elemento y revisar si tiene una proriedad  
Ejemplo: canvas  
```js
document.createElement('canvas').getContext
```
3. Crear un elemento, revisar si existe un metodo y probarlo  
Ejemplo: formatos de video  
```js
video.canPlayType(...)
```  
4. Crear un input, establecer un valor y comprobar si lo mantiene  
Ejemplo: nuevos tipos de `<input>`  

**3. Modernizr: la libteria para detectar HTML5**  
Incluyes Modernizr asi:  
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Dive Into HTML5</title>
  <script src="modernizr.min.js"></script>
</head>
<body>
  ...
</body>
</html>
```  
 Osea modernizr crea un objeto llamado **Modernizr**, con propiedades booleanas.  
 Ejemplo:  
 ```js
if (Modernizr.canvas) {
  // let's draw some shapes!
} else {
  // no native canvas support available :(
}
```   
**4. Detectar soporte de canvas**  
El canvas es un lienzo donde dibujas con JavaScript.  
Deteccion manual de canvas  
```js
function supports_canvas() {
  return !!document.createElement('canvas').getContext;
}
```  
Con Modernizr  
```js
if (Modernizr.canvas) {
  // let's draw some shapes!
} else {
  // no native canvas support available :(
}
```  
**5. Detectar soporte de texto en canvas**  
Aunque un navegador soporte canvas, puede NO soportar texto en canvas.  
Deteccion Manual   
```js
function supports_canvas_text() {
  if (!supports_canvas()) { return false; }
  var dummy_canvas = document.createElement('canvas');
  var context = dummy_canvas.getContext('2d');
  return typeof context.fillText == 'function';
}
```  
Con Modernizr  
```js
if (Modernizr.canvastext) {
  // let's draw some text!
} else {
  // no native canvas text support available :(
}
```  
**6. Video en HTML5**  
1. HTML5 introduce la etiqueta `<video>`, que permite poner videos sin usar plugins como Flash o QuickTime.  
2. Puedes poner varios archivos de video dentro de `<video>` y el navegador elegirá el que pueda reproducir.  
3. Si un navegador no soporta video HTML5, simplemente ignora la etiqueta; esto se puede aprovechar para usar un plugin como respaldo (ej. Video for Everybody).  
**7. Deteccion de soporte**  
Para saber si el navegador soporta video HTML5, se verifica si existe el método canPlayType() en un elemento `<video>`.  
Ejemplo de deteccion:  
```js
function supports_video() {
  return !!document.createElement('video').canPlayType;
}
```
La libreria Modernizr facilita estas funciones.  
**8. Formatos de video**  
Los navegadores no aceptan un solo formato estandar. Los principales son:  
1. Codec  
H.254 (mp4)  
Ogg Theora  
WebM (vp8/vorbis)

2. Ventajas  
Alta calidad, funciona en Safari y iPhone  
Libre  
Libre y moderno  

3. Navegadores  
Safari, Edge, algunos Chrome  
Firefox, navegadores libres  
Chrome, Firefox, Opera  

**9. HTML5 Local Storage**  
Local Storage permite guardar datos en tu navegador, similar a cookies pero con más espacio y sin enviarse al servidor.  
Se usa para almacenar información local en las páginas.  
Para saber si está disponible:  
```js
function supports_local_storage() {
  try {
    return 'localStorage' in window && window['localStorage'] !== null;
  } catch(e){
    return false;
  }
}
```  
**10. Web Workers**  
Web Workers  
Permiten ejecutar JavaScript en segundo plano sin bloquear la página.  
Útiles para tareas pesadas (cálculos, red, almacenamiento).  
Para saber si el navegador los soporta:
```js
!!window.Worker
```  
**11. Aplicaciones Web Offine**  
HTML5 permite que una web funcione sin conexión guardando archivos en el navegador.  
Sirve para apps tipo Gmail o Google Docs.  
El navegador descarga archivos necesarios y los usa cuando no hay internet.  
Para saber si se soporta:  
```js
!!window.applicationCache
```  
**12. Geolocalizacion**  
Permite saber la ubicación del usuario usando IP, WiFi, torres celulares o GPS.  
Aunque no es parte directa de HTML5, se adoptó al mismo tiempo.  
Para saber si se soporta la API:  
```js
!!navigator.geolocation
```  
Modernizr: Modernizr.geolocation.  
En navegadores viejos se puede usar Gears u otras APIs de teléfonos antiguos.  
  
**13. Nuevos Tipos de Input en HTML5**  
HTML5 añade muchos nuevos tipos de `<input>`, como:  
`<search>`,`<tel>`,`<url>`,`<email>`  
`<date>`,`<month>`,`<week>`,`<time>`,`<datetime-local>`  
`<number>`,`<range>`,`<color>`  
Como se detecta si un tipo de input es compatible  
1. Crear un input falso:  
```js
var i = document.createElement("input");
```  
2. Asignarle un tipo:  
```js
i.setAttribute("type", "color");
```  
3. Si el navegador no lo soporta el tipo regresa a "text"  
Modernizr facilita esto usando: Modernizr.inputtypes.  

**14. Placeholder**  
  
Es el texto gris que aparece dentro de un `<input>` cuando está vacío.  
Desaparece cuando haces clic.  
Para saber si el navegador lo soporta:  
```js
'placeholder' in document.createElement('input')
```  
Modernizr: Modernizr.input.placeholder.  

**15. Autofocus**  
  
HTML5 permite poner autofocus directamente en un input para que reciba el foco automáticamente.  
Más consistente que hacerlo con JavaScript.  
Para detectar si funciona:  
```js
'autofocus' in document.createElement('input')
```  
Modernizr: Modernizr.input.autofocus. 
   
**16. Microdatos**  
  
Sirven para añadir significado semántico al contenido (por ejemplo licencias, datos personales, etc.).  
Los buscadores pueden convertirlos en cosas como una vCard.  
El marcado funciona en todos los navegadores, pero la API del DOM no.  
Para saber si el navegador soporta la API:  
```js
!!document.getItems
```
Modernizr todavía no lo detecta.  
  
**17. History API**  
  
Permite modificar el historial del navegador sin recargar la página.  
Útil para SPA (Single Page Applications).  
Función clave: history.pushState().  
Para saber si está soportado:  
```js
!!(window.history && history.pushState)
```  
Modernizr: Modernizr.history.