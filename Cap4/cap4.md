**1. ¿Que es `<canvas>` en HTML5?**   
  
Lo que entendi de la lectura es un lienzo de mapa de bits (un rectángulo) donde puedes dibujar gráficos, animaciones, juegos, etc. usando JavaScript.  
De inicio es invisible, no tiene contenido ni borde hasta que tú lo dibujas.  
Cómo se usa  
```html
<canvas id="a" width="300" height="225"></canvas>
```  
Cada `<canvas>`:  
Es independiente.  
Mantiene su propio estado.  
Lo accedes con document.getElementById().  
  
**2. Obtener el contexto**  
  
Para dibujar necesitas el contexto 2D:
```js
var a_canvas = document.getElementById("a");
var ctx = a_canvas.getContext("2d");
```  
No hay contexto 3D estandarizado todavía, aunque podría venir en el futuro.  

**3. Dibujar formas simples**  
  
Los métodos básicos del contexto 2D son:  
fillStyle → Color o patrón de relleno.  
fillRect(x, y, w, h) → Dibuja un rectángulo sólido.  
strokeStyle → Color del borde.  
strokeRect(x, y, w, h) → Dibuja solo el borde.  
clearRect(x, y, w, h) → Borra esa zona del lienzo.  
  
Ejemplo del texto:  
```js
function draw_b() {
  var b_canvas = document.getElementById("b");
  var b_context = b_canvas.getContext("2d");
  b_context.fillRect(50, 25, 150, 100); 
}
```  

**4.¿Cómo reiniciar el lienzo?**  
  
Poniendo de nuevo su mismo ancho:  
```js
var b_canvas = document.getElementById("b");
b_canvas.width = b_canvas.width;
```  
Esto:  
Borra todo.  
Restaura las propiedades del contexto.  

**5. Sistema de coordenadas del canvas**  

El punto inicial es (0, 0) en la esquina superior izquierda.  
X aumenta hacia la derecha.  
Y aumenta hacia abajo.  
Ejemplo de declaración del canvas para dibujar ese sistema:  
```html
<canvas id="c" width="500" height="375"></canvas>
```  
Luego:  
```js
var c_canvas = document.getElementById("c");
var context = c_canvas.getContext("2d");
```  
Y ya puedes trazar líneas o dibujar lo que quieras.  

**6. Caminos en `<canvas>` de HTML5**  
  
1. ¿Qué es un “camino”?  
Un camino (path) es como un dibujo hecho con lápiz: lo defines, pero no aparece hasta que lo “entintas”.  
Para “dibujar” de verdad, se usa stroke() (tinta) o fill().  

**7. Métodos de "lápiz" (solo definen el camino)**  
  
moveTo(x, y) → mueve el lápiz al punto inicial.  
lineTo(x, y) → crea una línea desde el punto actual al nuevo punto.  
Estos no muestran nada aún en pantalla. Solo construyen el camino.  

**8. Métodos de “tinta” (dibujan el camino)**  
  
stroke() → dibuja las líneas del camino con el color actual.  
fill() → rellena el camino (para figuras cerradas).  
Color del trazo:  
```js
context.strokeStyle = "#eee";
```  

**9. Ejemplo de una cuadrícula**  
  
Osea se crean muchas líneas usando moveTo() y lineTo(), y después se dibujan todas juntas  
```js
context.stroke();
```  

**10. ¿Por qué usar coordenadas .5?**  
  
Para que las líneas tengan 1 píxel exacto de ancho.  
Ejemplo:  
Línea en x = 1 → se ve de 2 píxeles (mala).  
Línea en x = 1.5 → se ve de 1 píxel (correcta).  

**11. Crear un nuevo camino**  
  
Cuando quieres dibujar con otro color o empezar una figura diferente:  
```js
context.beginPath();
```  

**12. Dibujar texto en canvas**  
  
En canvas no hay CSS layout, solo dibujas texto en una posición.  
Propiedades importantes:  
font → igual que CSS ("bold 12px sans-serif").  
textAlign → start, end, left, right, center.  
textBaseline → top, middle, bottom, etc.  
Dibujar texto:  
```js
context.fillText("x", 248, 43);
```  

**13. Alineación del texto**  
  
Texto en esquina superior izquierda:  
```js
context.textBaseline = "top";
context.fillText("(0, 0)", 8, 5);
```  
Texto en esquina inferior derecha:  
```js
context.textAlign = "right";
context.textBaseline = "bottom";
context.fillText("(500, 375)", 492, 370);
```  

**14. Dibujar puntos**  
  
A falta de círculos, se usan pequeños rectángulos:  
```js
context.fillRect(0, 0, 3, 3);
context.fillRect(497, 372, 3, 3);
```  

**15. Gradientes en `<canvas>`**  
1. Tipos de gradientes  
  
El canvas soporta dos tipos:  
Lineales → cambian de color a lo largo de una línea (horizontal, vertical o diagonal).  
Radiales → cambian de color desde un círculo hacia otro.  
```js
createLinearGradient(x0, y0, x1, y1)
createRadialGradient(x0, y0, r0, x1, y1, r1)
```  

**16. Crear un degradado lineal**  
  
1. Creas el degradado:  
```js
var g = context.createLinearGradient(0, 0, 300, 0);
```  
2. Agregas paradas de color (0 a 1):  
```js
g.addColorStop(0, "black");
g.addColorStop(1, "white");
```  
3. Lo aplicas como relleno:  
```js
context.fillStyle = g;
context.fillRect(0, 0, 300, 225);
```  

**17. Cómo usar excanvas.js**  
  
En el `<head>` se agrega:  
```js
<!--[if lt IE 9]>
  <script src="excanvas.js"></script>
<![endif]-->
```  
Esto es un comentario condicional de IE.  
Solo IE8, IE7, etc. descargan y ejecutan ese script.  
Todos los demás navegadores lo ignoran → la página carga más rápido. 
   
Después de incluirlo:  
Puedes usar `<canvas>` normalmente.  
Puedes obtener el contexto con getContext("2d") y dibujar como siempre.  

Eso fue lo que entendi del capitulo 4