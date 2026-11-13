# Image-codificador
codificador de imagenes
## Codifica Imagenes hay que introducir la información en la selección
## Para agregar un efecto hover (al pasar el cursor por encima) sobre la imagen cargada, puedes usar transiciones de CSS (transition) y propiedades como transform, box-shadow o filter en tu regla 
## transition: ... 0.3s ease: Evita que el cambio sea brusco; hace que la animación dure 0.3 segundos de forma fluida tanto al entrar como al salir el cursor.
 ## transform: scale(1.05): Agranda la imagen un 5% sin empujar ni desacomodar los demás elementos de la página.
 ## box-shadow: Crea una ilusión de profundidad, haciendo que la imagen parezca levantarse de la pantalla.cursor: pointer: Cambia el puntero a una mano para dar retroalimentación visual al usuario.

 ## Para medir las dimensiones reales (ancho y alto en píxeles) y el peso del archivo cada vez que subes una imagen, puedes leer las propiedades naturalWidth y naturalHeight dentro del evento onload de la imagen, junto con file.size para los kilobytes o megabytes.

 ## imagePreview.naturalWidth y naturalHeight: Obtienen el ancho y alto originales de la imagen en píxeles, sin importar que por CSS la hayas limitado a 300px para la vista previa.

 ## file.size / 1024: Convierte el peso del archivo de bytes a kilobytes (KB).

 ## Orden dentro de onload: Es importante medir las dimensiones antes de ejecutar URL.revokeObjectURL(), asegurando que el navegador ya terminó de cargar el archivo en memoria.

 ## imagePreview. naturalWidth y  naturalHeight: Obtienen el ancho y alto originales de la imagen en píxeles, sin importar que por CSS la hayas limitado a 300px para la vista previa.

## file.size / 1024: Convierte el peso del archivo de bytes a kilobytes (KB).

 ## Orden dentro de onload: Es importante medir las dimensiones antes de ejecutar URL.revokeObjectURL(), asegurando que el navegador ya terminó de cargar el archivo en memoria.

## Para lograr que la imagen crezca a un ancho fijo en píxeles sin deformarse y manteniendo su proporción original, la clave está en definir únicamente el ancho (width o max-width) y dejar la altura en auto. Si fuerzas tanto un ancho como un alto fijos diferentes a la proporción de la foto, la imagen se estirará o se verá aplastada.
## Para mostrar la sección de información (dimensiones y peso) únicamente al pasar el cursor (hover) sobre la imagen, podemos envolver ambos elementos en un contenedor y usar CSS para ocultar la información por defecto y hacerla aparecer con una transición suave cuando el usuario haga hover.

## #imagePreview:hover + #imageInfo: El símbolo + selecciona el elemento inmediatamente siguiente en el HTML (#imageInfo) solo mientras el cursor esté encima de #imagePreview.
## transform: translateX(-15px) a translateX(0): Hace que el panel no solo aparezca gradualmente (opacity), sino que también se deslice suavemente hacia la derecha desde detrás de la imagen.

 ## pointer-events: none: Evita que el panel capture el mouse por accidente mientras aparece, asegurando que el hover no parpadee.
  ## Coordenadas reales vs. visuales: Como la imagen en pantalla se reduce a un máximo de 500px de ancho, el código calcula automáticamente la proporción (naturalWidth / rect.width) para entregarte las coordenadas exactas en píxeles de la imagen original.Arrastre multidireccional: Usando Math.min y Math.abs, el usuario puede arrastrar el mouse hacia abajo-derecha, arriba-izquierda o cualquier dirección sin que el rectángulo falle.Marcadores persistentes: Al presionar "Guardar Sección", el recuadro punteado rojo se convierte en un recuadro azul fijo con su etiqueta encima para que el usuario vea qué áreas ya registró.Efecto Hover Interactivo (.saved-box:hover): Al pasar el cursor sobre cualquier rectángulo azul dibujado en la imagen, este se remarca con un tono más intenso Tooltip Flotante (.tooltip-info): Muestra un cuadro flotante con la información completa de esa sección (nombre, dato asociado y sus medidas exactas en píxeles) de manera limpia y sincronizada con el mouse.Empaqueta la codificación: Al hacer clic en "Descargar Codificación (JSON)", se crea un archivo JSON estructurado que incluye el nombre del archivo de la imagen, sus dimensiones reales totales en píxeles y todas las secciones mapeadas con sus nombres, valores y coordenadas exactas (x, y, width, height).Descarga automática: El navegador descarga el archivo listo para que lo uses en bases de datos, entrenamientos de machine learning o análisis posterior.
  ## Para guardar tanto la imagen (PNG) como toda su codificación de secciones (JSON) en un solo archivo descargable —y además poder volver a cargarlo en tu aplicación— la mejor estrategia es convertir la imagen a texto mediante Base64 (Data URL) e incrustarla directamente dentro del objeto JSON.

   ## De este modo, obtienes un único archivo .json autocontenido que guarda la imagen original intacta y todas sus coordenadas. Al volver a subir ese archivo, se restauran tanto la imagen como los recuadros interactivos en un solo paso.
   ## Estandarización a PNG: Al subir cualquier imagen, un elemento <canvas> oculto la procesa y la convierte mediante canvas.toDataURL('image/png') en una cadena de texto Base64 garantizada en formato PNG sin pérdida.

   ## Descarga con Blob: Como la cadena Base64 de una imagen puede ser larga, usamos new Blob([...]) en lugar de una URL data:text/json tradicional para evitar límites de longitud del navegador al descargar el archivo.

  ## Restauración en 1 clic: Cuando seleccionas el archivo _mapeo_completo.json en el segundo input, la aplicación extrae la imagen directamente desde imagenBase64 y dibuja encima todas tus secciones en sus coordenadas exactas, sin que tengas que volver a buscar la imagen por separado.