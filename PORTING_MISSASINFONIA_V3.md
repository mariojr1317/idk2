# Preparación de port HTML5: FNF VS Missasinfonia v3

Estado: **preparación e inventario; todavía no es un port HTML5 jugable**.

## Fuente revisada

- Archivo: `fnf_vs_missasinfonia_v3_fe527.zip`
- Contenido: 809 archivos (886 entradas incluyendo carpetas).
- Tamaño total descomprimido: aproximadamente 217,6 MB.
- Estructura típica de un paquete de mods de Psych Engine: `characters/`, `custom_events/`, `custom_notetypes/`, `data/`, `fonts/`, `images/`, `music/`, `scripts/`, `shaders/`, `songs/`, `sounds/`, `stages/`, `videos/` y `weeks/`.

## Inventario

| Área | Archivos |
|---|---:|
| images | 340 |
| data | 127 |
| custom_events | 125 |
| stages | 59 |
| characters | 55 |
| songs | 40 |
| scripts | 13 |
| sounds | 13 |
| weeks | 10 |
| videos | 9 |
| music | 6 |
| fonts | 3 |
| shaders | 3 |
| custom_notetypes | 2 |
| metadatos/otros | 4 |
| **Total** | **809** |

Extensiones detectadas: 241 PNG, 178 Lua, 150 JSON, 88 TXT, 83 XML, 56 OGG, 8 MP4, 2 TTF, 2 FRAG y 1 HX.

## Lo que comprobé del repositorio destino

Este repo publica una exportación HTML5 compilada mediante `index.html` y `PsychEngine.js`. También incluye archivos de manifiesto como `manifest/default.json`, `manifest/shared.json`, `manifest/songs.json` y `manifest/videos.json`. No basta con copiar el ZIP a una carpeta y asumir que una build web ya compilada descubrirá todos los archivos del mod.

La exportación que existe en el repositorio contiene principalmente recursos bajo `assets/` (por ejemplo `assets/characters/`, `assets/data/`, `assets/images/`, `assets/songs/`, `assets/stages/` y `assets/weeks/`). Es necesario comprobar y, según el cargador utilizado, reconstruir los manifiestos para incluir los nuevos recursos. No encontré en la raíz los archivos fuente habituales de compilación Haxe/OpenFL/Lime (como `Project.xml`) para reconstruir el motor desde aquí.

## Incompatibilidades que deben resolverse antes de declarar el port terminado

1. **Scripts Lua/HScript/Haxe:** hay 178 archivos Lua y un archivo Haxe (`scripts/VideoSpriteHandler.hx`). Las funciones de sistema/escritorio y las dependencias nativas pueden no funcionar en navegador. Cada script debe auditarse y probarse; no se deben borrar silenciosamente los que no sean portables.
2. **Vídeos:** hay 8 MP4 y la referencia Haxe para sprites de vídeo puede requerir una alternativa compatible con navegador. El vídeo más grande mide aproximadamente 65 MB.
3. **Audio:** el paquete usa OGG mientras la exportación web actual incluye pistas MP3 en su manifiesto de canciones. Se debe comprobar la ruta/formato que usa el código compilado y agregar los archivos correctos al manifiesto.
4. **Nombres compartidos:** el paquete incluye definiciones como `bf.json` y `gf.json`. Aplanar sus archivos en `assets/` podría sobrescribir recursos del juego base; se debe preservar el aislamiento del mod o revisar deliberadamente cada conflicto.
5. **Weeks y freeplay:** las semanas del mod y las charts deben enlazarse a los datos que la exportación HTML5 realmente carga.
6. **Permisos y derechos:** conservar los créditos y respetar la licencia/permiso de distribución del mod antes de redistribuir todos sus recursos.

## Ruta recomendada para la integración final

- Mantener el mod aislado, inicialmente con la estructura `mods/FNF VS Missasinfonia v3/` como copia de referencia.
- Adaptar los recursos portables a las rutas que reconoce esta exportación HTML5, sin sobrescribir archivos base por accidente.
- Actualizar/regenerar los manifiestos para characters, charts, imágenes, audio, vídeos y demás recursos realmente usados.
- Auditar scripts que utilicen shaders, vídeo, estados personalizados, acceso al sistema o APIs no disponibles en HTML5.
- Probar desde GitHub Pages una canción por vez, empezando por una chart sencilla; después probar semanas, stages, eventos, diálogos y vídeos.

## Límite de esta rama

Esta rama registra el análisis y el plan; **no declara que los 809 archivos ya estén subidos ni que el juego los esté cargando**. La conexión de GitHub disponible aquí permite editar archivos de texto, pero no proporciona una transferencia masiva de los 217 MB de recursos binarios del ZIP. La exportación compilada tampoco ofrece aquí un proyecto fuente con el que volver a compilar el motor. Por tanto, se necesita una vía de transferencia de los binarios y una prueba de la integración de manifiestos antes de producir una build jugable.
