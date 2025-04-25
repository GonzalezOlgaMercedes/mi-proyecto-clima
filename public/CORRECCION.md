PROBLEMA: el contenido del index.html se veía horrible porque no se estaba aplicando el css del index.css
SOLUCIÓN: linkear el css haciendo <link rel="stylesheet" href="index.css"> en el head.

PROBLEMA: el archivo css se llama index.css, por convención los archivos css se los nombra styles.css, estilos.css y similares.
SOLUCIÓN: cambiar el nombre del archivo nombrándolo con los nombres convencionales, en este caso optaremos por *styles.css* (se prefiere los nombres en inglés).
NOTA: al renombrar el archivo debemos considerar los lugares dentro del documento que los estén utilizando, por lo que ahora tendríamos <link rel="stylesheet" href="styles.css"> en el head.

PROBLEMA: la información no se actualiza automáticamente porque los datos están cargados manualmente.
SOLUCIÓN: hacer uso de APIs como Weather API por ejemplo.

PROBLEMA: en el index.html se hace un linkeo a <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css" /> que no se usa, al quitarlo no hay cambios visuales ni funcionales. Para confirmarlo hemos inspeccionado en el navegador (Chrome) con DevTools (F12) en la pestaña Coverage en el que podemos ver que “leaflet.min.css” aparece con 100 % de bytes sin usar (10 879 de 10 879), así que el Coverage nos está diciendo que ninguna de sus reglas se aplicó en el DOM al cargar la página. Para más detalle ver la imagen **unusedBytes.png**
SOLUCIÓN: quitar la referencia e incluirlo más adelante en caso de necesitarlo.

PROBLEMA: caracter no válido o malformado. En la línea 251 del index.html se encontró esta estructura <span class="map-legend__label">Muy frío (< 0°C)</span>, aquí el problema en particular es (< 0°C) donde el anvegador lo confunde con el inicio de una etiqueta pero “después de <” no había un identificador válido, así que lanza el error.
SOLUCIÓN: La forma adecuada de mostrar el signo "menor que" no es escribirlo directamente sino usar la entidad de carater (character entity) &lt; Se usa así para que el navegador muestre < en la página en lugar de interpretarlo como el inicio de una etiqueta HTML. Por lo que ahora la línea 251 quedaría así <span class="map-legend__label">Muy frío (&lt; 0°C)</span>
NOTA: para hallar este error particular se utilizó W3C Validator (tanto para el HTML como el CSS).

PSEUDO-PROBLEMA: Hay iconos declarados en CSS como .icon-snowy, .icon-stormy o .icon-visibility entre otros que no aparecen en el HTML. Cada sentencia extra ralentiza la carga y el mantenimiento. 
SOLUCIÓN: si el archivo CSS es compartido puede que otros archivos sí utilicen esas y otras sentecias CSS.