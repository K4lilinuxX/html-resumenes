**1. Contenedores de video**  
  
El resumen lo que entendi es:  
Un contenedor es como un ZIP que guarda dentro:  
° Pistas de video  
° Pistas de audio  
° Metadatos  
  
Los más comunes:  
  
° MP4 (.mp4 / .m4v / .mov) – Muy usado, soporta H.264 + AAC.  
° FLV (.flv) – El de Flash.  
° Ogg (.ogv) – Libre, soporta Theora + Vorbis.  
° WebM (.webm) – Nuevo, libre, usa VP8 + Vorbis.  
° AVI (.avi) – Antiguo, poco flexible.  

**2. Códecs de video**  
  
El códec define cómo se comprime el video.  
Los tres importantes:  
1. H.264  
° Excelente calidad, usado en YouTube y Blu-Ray    
° Súper compatible (iPhone, Android, Safari, Flash)  
° Patentado → tiene costos de licencia  

2. Theora  
° Libre, abierto  
° Se usa con contenedor Ogg    
° Soportado por Firefox, Opera, Chrome (viejas versiones)  

3. VP8  
° Libre, creado por Google  
° Se usa en WebM  
° Soportado por Chrome, Firefox y Opera  

**3. Códecs de audio**  
  
Los que importan para web:  
1. MP3  
Muy común; 2 canales; patentado  
2. AAC  
Mejor calidad que MP3; usado por Apple y H.264; patentado  
3. Vorbis  
Libre; va en Ogg o WebM  
  
**4. ¿Qué soporta cada navegador?**  
  
No existe un solo formato que funcione en todos los navegadores  
  
Ejemplos:  
  
° Firefox / Opera / Chrome: Ogg (Theora + Vorbis) y WebM  
° Safari y iPhone: MP4 (H.264 + AAC)  
° Internet Explorer 9: MP4 (H.264 + AAC)  
° Android: MP4 (H.264 + AAC), algunos WebM  

**5. La conclusión fuerte**  
  
Para que tu video funcione en todos lados, debes generarlo 3 veces:  
1. WebM (VP8 + Vorbis)  
2. MP4 (H.264 + AAC)  
3. Ogg (Theora + Vorbis)  

Y ponerlos juntos en un solo `<video>` para que el navegador elija el que pueda reproducir.  
Además, para compatibilidad total con navegadores viejos (IE8 y otros), debes poner un fallback en Flash.  

**6. Problemas de licencias**  
  
° H.264 cuesta dinero a las empresas que distribuyen videos grandes  
° Esto afecta televisiones por internet, empresas y plataformas de streaming  
° Por eso hay debate entre usar códecs libres (WebM / Theora) o seguir con H.264  

**7. Codificar video con Miro Video Converter**  
  
° Miro Video Converter es un programa gratuito y de código abierto que convierte videos a varios formatos sin opciones avanzadas  
  
° Solo haces:  
1. Abrir Miro  
2. Elegir tu archivo de video  
3. Elegir un formato de salida  
4. Presionar Convertir  

° Los 3 formatos importantes para HTML5 son:  
1. WebM (VP8 + Vorbis)  
2. Theora (Ogg)  
3. H.264 (MP4 para iPhone)  

° Debes convertir tu video tres veces, una para cada formato.  
Los archivos se guardan junto al video original con nombres como:  
° SOURCEFILE.webm  
° SOURCEFILE.theora.ogv  
° SOURCEFILE.iphone.mp4  

Cuando ya tengas los 3 archivos, puedes usarlos juntos dentro de un `<video>` en HTML.  

**8. Codificar Ogg Video con Firefogg**  
  
° Firefogg es una extensión de Firefox (gratuita y open source) para convertir videos a Ogg Theora, que funciona en navegadores como Firefox y Chrome  

° Pasos:  
1. Instalar Firefogg desde su sitio  
2. Abrir la opción Make Ogg Video  
3. Seleccionar tu archivo de video  

° Firefogg tiene varias pestañas, pero solo importa una:  
°Basic quality and resolution control  
Aquí ajustas:  
° Calidad de video (0–10)  
° Calidad de audio (–1 a 10)  
° Códecs (siempre: video = theora, audio = vorbis)  
° Tamaño del video (puedes cambiar ancho y automáticamente ajusta el alto)  

° Cuando estés listo, presionas Save Ogg, eliges nombre, y esperas a que termine la codificación.  
  
**9. Codificar muchos videos Ogg/Theora con ffmpeg2theora**  
El texto explica cómo codificar videos para la web usando herramientas más avanzadas, especialmente desde línea de comandos, ideal para automatizar procesos o trabajar con muchos archivos  
  
Se cubren 3 tipos principales de codificación:  
1. Ogg/Theora (para Firefox y Chrome)  
2. H.264 (para Safari, iPhone, Android, Flash)  
3. WebM/VP8 (formato moderno de Google)  
  
° ffmpeg2theora es una herramienta open-source para generar videos Ogg (Theora + Vorbis)  
° Funciona en Windows, Mac y Linux  
° Se usa desde la terminal  
° Permite automatizar la conversión de muchos videos (ideal para “batch encoding”)  
  
Parámetros importantes:  
° --videoquality 0–10 → calidad del video  
° --audioquality -2–10 → calidad del audio  
° --max_size WxH → redimensionar video manteniendo proporción  
  
Ejemplo de uso:  
```css
ffmpeg2theora --videoquality 5 --audioquality 1 --max_size 320x240 pr6.dv
```  
Genera: pr6.dv.ogv  
  
2. Codificar video H.264 con HandBrake  
HandBrake ahora se centra casi solo en H.264 (MP4)  
Ideal para Safari, iPhone, Android, Flash  
  
Tiene versión gráfica y versión por terminal (HandBrakeCLI)  
Versión gráfica:  
° Abrir video → elegir preset “iPhone & iPod Touch”  
° Activar “Web Optimized” (muy recomendado)  
° Ajustar resolución manteniendo proporciones  
° En la pestaña Video:  
° Códec: H.264  
° Activar 2-pass encoding (mejor calidad)  
° Opcional: turbo first pass  
° Ajustar calidad/bitrate  
Finalmente: elegir nombre del archivo → Start  
  
Versión por terminal:  
Se puede automatizar igual que con ffmpeg2theora  

```css
HandBrakeCLI --preset "iPhone & iPod Touch" --width 320 --vb 600 \
--two-pass --turbo --input pr6.dv --output pr6.mp4
```  
  
3. Codificar WebM (VP8 + Vorbis) con ffmpeg  
° Requiere versión de ffmpeg compilada con:
° --enable-libvpx (VP8)  
° --enable-libvorbis  
  
Se usa codificación de dos pasadas:  
1. Primera pasada: analiza el video  
2. Segunda pasada: codifica realmente  
  
Ejemplo 1:  
Pasada 1:  
```css
ffmpeg -pass 1 -passlogfile pr6.dv -i pr6.dv -vcodec libvpx \
-b 614400 -s 320x240 -aspect 4:3 -an -y NUL
```  
Posada 2:  
```css
ffmpeg -pass 2 -passlogfile pr6.dv -i pr6.dv -vcodec libvpx \
-b 614400 -s 320x240 -aspect 4:3 -acodec libvorbis -y pr6.webm
```  
Parámetros clave:  
° libvpx → video VP8 (WebM)  
° libvorbis → audio Vorbis  
° -b → bitrate (en bits, no kbps)  
° -s → tamaño del video  
° -aspect → relación de aspecto  

**10. Formas básicas de usar `<video>`**  
  
Puedes poner un solo archivo así:  
```html
<video src="video.webm"></video>
```  
Debes incluir width y height para definir el tamaño del cuadro  

**11. Controles y atributos útiles**  
  
° controls → muestra controles del reproductor  
° preload → indica si el navegador debe descargar el video al cargar la página  
° preload o preload="auto" = empieza a descargar  
° preload="none" = no descarga hasta que el usuario interactúe  

**12. Usar varios formatos de video**  
  
Para máxima compatibilidad, se recomienda incluir tres formatos:  
.mp4 → H.264 (muy compatible)  
.webm → VP8/VP9  
.ogv → Theora  
Ejemplo:  
```html
<video width="320" height="240" controls>
  <source src="video.mp4"  type='video/mp4; codecs="avc1.42E01E, mp4a.40.2"'>
  <source src="video.webm" type='video/webm; codecs="vp8, vorbis"'>
  <source src="video.ogv"  type='video/ogg; codecs="theora, vorbis"'>
</video>
```  
El navegador elegirá el primero que pueda reproducir sin descargar los otros  

**13. MIME Types (muy importante)**  
  
El servidor debe mandar los videos con el tipo MIME correcto, si no no se reproducen aunque tu HTML esté bien:  
```bash
AddType video/ogg .ogv
AddType video/mp4 .mp4
AddType video/webm .webm
```  
**14. Compatibilidad con navegadores**  
  
Internet Explorer  
° IE9 soporta `<video>` y H.264.  
° IE8 y anteriores → usar Flash como fallback.  
° Se hace metiendo un `<object>` dentro del `<video>`  
  
iOS (iPhone/iPad)  
° iOS 3.x tenía bugs:  
° No soportaba poster  
° Solo reconocía la primera fuente `<source>`  
° Todo esto se arregla desde iOS 4  

Android  
° Antes de Android 2.3 había problemas:  
° No funcionaba bien el atributo type  
° controls no era soportado  
° Solo reproducía MP4  

**15. Ejemplo completo**  
  
Incluye:  
° HTML5 video  
° fallback a Flash  
° click para reproducir/pausar en Android
  
Ese seria mi resumen de la lectura del capitulo 5 del libro de HTML