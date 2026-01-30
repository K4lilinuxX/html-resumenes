**Aplicaciones Web Offline (Dive Into HTML5)**.  

**¿De qué trata este capítulo?**.  
Este capítulo trata de cómo hacer que una **aplicación web funcione sin conexión a internet**, usando características de HTML5. La idea es que el navegador pueda cargar archivos y datos incluso cuando el usuario está offline.

**El problema de las apps web tradicionales**.  
Las aplicaciones web normales:
- Dependen completamente de internet
- Dejan de funcionar si no hay conexión
- Pierden datos si el usuario se desconecta

HTML5 introduce soluciones para evitar esto.

**¿Qué es una aplicación web offline?**.  
Es una web que:
- Puede cargarse sin internet
- Guarda archivos localmente
- Mantiene el estado de la aplicación
- Funciona como si fuera una app nativa

**El Application Cache (AppCache)**.  
HTML5 introduce **Application Cache**, que permite:
- Descargar y guardar archivos localmente
- Definir qué recursos se usan offline
- Controlar qué se actualiza y cuándo

Nota: AppCache fue revolucionario, pero también problemático y hoy está **obsoleto** (reemplazado por Service Workers).

**El archivo Manifest**.  
El corazón del modo offline es el **archivo manifest**.

Contiene:
- Lista de archivos que deben cachearse
- Recursos que requieren internet
- Recursos alternativos si no hay conexión

Ejemplo de secciones:
- `CACHE`
- `NETWORK`
- `FALLBACK`

**Cómo funciona el cacheo**.  
El navegador:
1. Descarga el manifest
2. Cachea todos los recursos listados
3. Usa esos archivos cuando no hay conexión
4. Solo actualiza el cache si el manifest cambia

Un pequeño cambio en el manifest fuerza la actualización.

**Actualización del cache**.  
Puntos clave:
- El cache **no se actualiza automáticamente**
- El usuario puede estar usando una versión vieja
- Se necesita lógica adicional para recargar la app

Esto causó muchos dolores de cabeza a los desarrolladores.

**Eventos del Application Cache**.  
AppCache incluye eventos como:
- `checking`
- `downloading`
- `progress`
- `cached`
- `updateready`
- `error`

Estos permiten saber qué está pasando con el cache.

**Riesgos y limitaciones**.  
Problemas comunes:
- Difícil de depurar
- Comportamiento impredecible
- Fácil dejar a usuarios “atrapados” en versiones viejas

Por eso fue reemplazado.

**Evolución: el camino a Service Workers**.  
El capítulo deja claro que:
- AppCache fue un primer intento
- Sentó las bases para apps offline modernas
- Dio paso a tecnologías mejores como **Service Workers**

**Idea clave del capítulo**.  
HTML5 permitió por primera vez:
- Webs que funcionan sin internet
- Experiencias tipo app nativa
- Almacenamiento local de recursos

Aunque AppCache ya no se usa, fue un paso crucial.

**Conclusión**.  
Este capítulo muestra el inicio de:
- Progressive Web Apps (PWA)
- Apps web modernas
- Experiencias offline reales

Es un capítulo histórico que explica **cómo empezó la web offline**.
