**ESTÁS AQUÍ (Y TODOS LOS DEMÁS TAN)**  
  
Lo que entendi es que la ubicación (geolocalización) es la forma de saber dónde se encuentra un usuario en el mundo, usando métodos como la IP, redes Wi-Fi, torres celulares o GPS. Compartir esta información siempre es opcional y requiere el permiso explícito del usuario, por temas de privacidad.  

Osea la API de Geolocalización permite que los sitios web obtengan la latitud y longitud del usuario para funciones como mostrar mapas o buscar lugares cercanos. Es compatible con la mayoría de los navegadores modernos en computadoras y dispositivos móviles.  

Cuando un sitio intenta obtener la ubicación, el navegador muestra una barra de autorización donde el usuario puede aceptar, rechazar o guardar su decisión. El sitio web no puede acceder a la ubicación hasta que el usuario responda.  

En JavaScript, la geolocalización se usa mediante `navigator.geolocation.getCurrentPosition()`, que funciona de manera asíncrona y devuelve los datos en una función callback. Esta función recibe un objeto `position`, que incluye información como latitud, longitud, precisión y tiempo. Solo algunas propiedades están garantizadas; otras dependen del dispositivo y su hardware.  

**Manejo de errores y opciones en la API de Geolocalización**. 

La geolocalización puede fallar por varias razones, y el usuario siempre tiene el control. Si no da permiso, la aplicación no puede obtener su ubicación. En código, los errores se manejan pasando una función de error como segundo argumento de `getCurrentPosition()`.  

Cuando ocurre un error, se recibe un objeto PositionError, que incluye:  
1. PERMISSION_DENIED (1): el usuario rechazó compartir su ubicación.   
2. POSITION_UNAVAILABLE (2): no se pudo obtener la ubicación (red caída o sin señal GPS).  
3. TIMEOUT (3): tardó demasiado en calcularse la posición.  

La API usa el sistema de coordenadas WGS84, que solo funciona para la Tierra. Por eso sirve en la Estación Espacial Internacional, pero no en la Luna ni otros planetas.  

**Precisión de la ubicación**.  

Los dispositivos pueden obtener la ubicación de dos formas:  
1. Baja precisión: usando torres celulares (rápido, menos exacto).  
2. Alta precisión: usando GPS (muy exacto, pero más lento y consume más batería).  

No todas las aplicaciones necesitan alta precisión. Por ejemplo:  
1. Buscar cines cercanos → baja precisión es suficiente.  
2. Navegación paso a paso → alta precisión es necesaria.  

**Opciones de getCurrentPosition()**.  

Se puede pasar un tercer argumento con opciones:  
1. enableHighAccuracy: pide mayor precisión (puede ser más lento o fallar).  
2. timeout: tiempo máximo de espera para obtener la ubicación.  
3. maximumAge: permite usar una ubicación guardada en caché si aún es reciente.  

Usar caché evita recalcular la ubicación y ahorra recursos.  

**watchPosition()**.  
Si necesitas la ubicación de forma continua, se usa `watchPosition()`:  
1. Llama a la función de éxito cada vez que cambia la ubicación.  
2. Ideal para mapas en tiempo real o navegación.  
3. Devuelve un ID que se puede usar con `clearWatch()` para detener el seguimiento.  

**Geolocalización en IE y navegadores antiguos**.  

Antes de Internet Explorer 9, IE no soportaba la API de geolocalización del W3C. Para solucionar esto existía Google Gears, un complemento de código abierto que añadía funciones modernas (incluida la geolocalización) a navegadores antiguos en varias plataformas.  

Además, muchos dispositivos móviles viejos (BlackBerry, Nokia, Palm, etc.) tenían sus propias APIs de geolocalización, todas diferentes entre sí, lo que hacía el desarrollo más complicado.  

**geo.js: la solución**.  
geo.js es una librería JavaScript de código abierto que unifica:  
1. La API de geolocalización W3C.  
2. La API de Google Gears.  
3. APIs de plataformas móviles antiguas.  

Así el desarrollador usa una sola forma de acceder a la ubicación, sin preocuparse por el navegador o dispositivo.  

Para usarla:  
1. Se incluyen los scripts `gears_init.js` y `geo.js` al final del HTML.  
2. Se llama a `geo_position_js.init()` para verificar si hay soporte.  
3. Luego se usa `getCurrentPosition()` para obtener la ubicación.  

**Uso básico**.  
1. `init()` → solo verifica si es posible usar geolocalización.  
2. `getCurrentPosition(success, error)` → pide permiso al usuario y obtiene la ubicación.  
3. La función de éxito recibe un objeto con latitud y longitud.  
4. La función de error se ejecuta si el usuario rechaza o ocurre un fallo.  

Limitación importante.  
`geo.js` NO soporta `watchPosition()`, así que si necesitas ubicación en tiempo real debes llamar manualmente a `getCurrentPosition()` varias veces.  

**Ejemplo completo de geolocalización con geo.js**.  

Este ejemplo muestra cómo usar geo.js para obtener la ubicación del usuario y mostrarla en un mapa.  
**Cómo funciona**  
1. Al cargar la página, se llama a `geo_position_js.init()` para verificar si el navegador admite geolocalización (ya sea por la API W3C, Gears o APIs antiguas).  
2. Si hay soporte, se muestra un enlace o botón que el usuario puede presionar para buscar su ubicación.   
3. Al hacer clic, se ejecuta `lookup_location()`, que llama a:  
```js
geo_position_js.getCurrentPosition(show_map, show_map_error);
```  

**Si la ubicación se obtiene correctamente**.  

* Se llama a la función `show_map(loc)`.  
* loc.coords contiene:
   * latitud
   * longitud
   * precisión (aunque en el ejemplo no se usa).  
* Se usa la API de Google Maps para:
   * Crear un mapa
   * Centrarlo en la ubicación del usuario
   * Añadir controles de navegación
   * Colocar un marcador con el mensaje “You are here”.  

**Si ocurre un error**.
* Se ejecuta show_map_error().  
* Se muestra un mensaje indicando que no se pudo determinar la ubicación.  

**Idea clave del ejemplo**.  
* geo.js simplifica la compatibilidad entre navegadores viejos y nuevos.
* El usuario siempre debe dar permiso.
* La geolocalización se puede integrar fácilmente con mapas para mostrar información visual útil.  

**Cierre**.  
El capítulo concluye recomendando documentación adicional sobre APIs de geolocalización y señalando que el contenido forma parte del libro HTML5: Up & Running.