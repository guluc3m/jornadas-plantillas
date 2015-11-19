<!-- Front page -->
\topskip200pt

\begin{center}

\Huge\center
Grupo de Usuarios de Linux

\huge
Cómo usar la plantilla de presentaciones para las Jornadas Técnicas

\end{center}

\clearpage
\topskip0pt
\renewcommand{\contentsname}{Contenido de este documento}
\tableofcontents
\clearpage

<!-- Document -->
# Qué se proporciona

En este directorio se proveen:

- `beamerthemesimple.sty`: El documento que contiene el tema de LaTex que le da forma a las presentaciones^[\ El tema está basado en una versión modificada del tema `Simple`, creado por Facundo Muñoz y disponible en <https://github.com/famuvie/beamerthemesimple>.].
- `demo.tex`: Un documento \LaTeX\ que muestra la sintaxis básica para la creación de diapositivas.
- `demo.pdf`: El documento PDF producto de la compilación del documento anterior.
- `presentacion.tex`: El documento \LaTeX\ cuya intención es servir como plantilla para las presentaciones que preparen los ponentes.
- `instrucciones.pdf`: La documentación con instrucciones sobre cómo usar la plantilla preparada para las presentaciones de las Jornadas Técnicas del GUL, en formato PDF.
- `instrucciones.md`: El documento con sintaxis Markdown que da origen a las instrucciones en PDF^[\ El documento en PDF ha sido generado utilizando Pandoc. Puedes encontrar una breve introducción a Pandoc en la presentación que hizo Rafael Medina para las XXVI jornadas, disponible en <http://archive.rmedgar.com/talks/pandoc_markdown/>.]. Por si no usas interfaz gráfica y prefieres leer el documento desde la terminal. Al fin y al cabo, todos sabemos que un auténtico linuxero lo hace todo desde la terminal.
- El directorio `img/`: Contiene el logo del GUL (`logo1.png`). También puedes utilizar este directorio para las imágenes que incluyas en tu propia presentación.

Realmente, para utilizar la plantilla para preparar tu presentación tan solo necesitas los siguientes contenidos:

- `beamerthemesimple.sty`.
- `presentacion.tex` (puedes renombrar el fichero como te plazca).
- `img/logo1.png`.

El resto de contenidos pretenden tener una función ilustrativa sobre el funcionamiento y la utilización de la plantilla.

\clearpage

# Cómo utilizar la plantilla

## Requerimientos

La plantilla utiliza para la generación del PDF a partir del documento \LaTeX\, evidentemente, `latex`. Más concretamente, para la compilación a PDF es necesario el paquete `pdflatex`. Si utilizas la versión ligera de `latex`, es posible que no tengas el paquete `pdflatex` instalado. Si utilizas `MacTeX`, la versión completa del paquete ya incluye `pdflatex`. El paquete `pdflatex` tiene equivalentes que también permiten la compilación de documentos \LaTeX\ a PDF; usa el que te plazca.

Para la generación de diapositivas, se utiliza la clase de documento `Beamer`.

Para el estilo del documento generado, se utiliza el tema modificado `Simple` (ver primera nota al pie).

Este documento da por hecho que sabes trabajar con /LaTeX/ para la generación de diapositivas o que, en su defecto, eres capaz de buscarte la vida con la información proporcionada, como los auténticos linuxeros.

## Utilización de la plantilla

Para utilizar la plantilla en tu presentación, tan solo tienes que abrir el documento `presentacion.tex` en tu editor predilecto (que no sea Gedit) y modificarlo de la siguiente manera:

- Cambia el texto "`Tu titulo`" en la línea donde pone `\title{Tu titulo}` por el título de tu charla.
- Cambia el texto "`Tu subtitulo`" en la línea donde pone `\subtitle{Tu subtitulo}` por el subtítulo de tu charla. Si tu charla no tiene subtítulo, puedes dejar el texto entre llaves en blanco.
- Cambia el texto "`Tu nombre`" en la línea donde pone `\author{Tu nombre}` por tu nombre. Si no quieres que aparezca tu nombre en la portada de la presentación, de nuevo puedes también dejar en blanco el texto entre llaves. Si sois varios ponentes, podéis utilizar la sintaxis de \LaTeX\ que consideréis oportuna para que aparezcan vuestros nombres de una manera bonita en la portada de la presentación.
- Prepara tu presentación añadiendo las diapositivas que consideres oportunas. Un comentario bien grande en el documento indica el inicio de la presentación como tal. Ya hay escritas una diapositiva inicial con la tabla de contenidos y una diapositiva en blanco. Puedes cargarte la diapositiva con la tabla de contenidos si no la consideras relevante para tu presentación.

Si tienes dudas sobre la sintaxis básica para la generación de diapositivas usando \LaTeX\, siempre puedes recurrir a la pequeña demo `demo.tex` que acompaña a este documento. `demo.pdf` muestra cómo quedan las cosas.

La plantilla por defecto está configurada para generar las diapositivas en ratio de aspecto 4:3, ya que es el ratio de aspecto de los proyectores de la universidad. Sin embargo, si quieres utilizarla para otros ratios de aspecto, tan solo tienes que cambiar la primera línea de la presentación. Por ejemplo, si quisieras trabajar con formato 16:9 (estándar widescreen), simplemente tendrías que cambiar `\documentclass[aspectratio=43]{beamer}` por `\documentclass[aspectratio=169]{beamer}`.

## Generación del PDF con la presentación

De nuevo, suponemos que sabes generar presentaciones a partir de documentos \LaTeX\. Si no, ya sabes, `GIYF`.

Pero vamos, que de todas formas el asunto es tan simple como ejecutar el siguiente comando:

```
$> pdflatex presentacion.tex
```
Si no te gusta `pdflatex` por alguna razón o tienes instalado un paquete que hace lo mismo y no te apetece instalar `pdflatex`, usa el comando que prefieras.

Es posible que a la hora de generar el pdf final (que se llamará `presentacion.pdf` y se encontrará en el mismo directorio que `presentacion.tex`) la diapositiva con la tabla de contenidos se haya quedado en blanco. Es curioso el por qué esto pasa. Lo importante es que te quedes tranquilo: no estás loco, es normal. [Aquí](http://stackoverflow.com/questions/3863630/latex-tableofcontents-command-always-shows-blank-contents-on-first-build) tienes un hilo de StackOverflow que trata el tema por si tienes curiosidad.

También, en el proceso de generación del PDF final, se generarán un montón de ficheros necesarios en el proceso.

Una solución cutre pero efectiva a estos dos problemas es simplemente usar la siguiente secuencia de comandos:

```
$> pdflatex presentacion.tex; pdflatex presentacion.tex
$> find . -type f \( -iname \*.aux -o -iname \*.log -o -iname \*.nav 
   -o -iname \*.out -o -iname \*.snm -o -iname \*.toc \) -delete
```

Si te aburres y te apetece currarte un script que proporcione una solución más elegante, no dudes en mandarnos tu pull request.

Si la anterior solución no solo te parece cutre sino que además conoces una solución más elegante sin necesidad de scripts, no dudes en mandarnos tu pull request también con la versión corregida de este documento. O puedes unirte a la lista de correo del GUL^[\ <https://gul.uc3m.es/mailman/listinfo/gul>] y comentarlo por ahí.

\clearpage

# Y ahora, ¿qué?

Bueno, pues a estas alturas ya deberías tener una bonita presentación, `presentacion.pdf`. Ya solo te queda venir a las Jornadas y dar tu charla y dejar a los cientos de asistentes^[\ El número de asistentes no está garantizado.] boquiabiertos con tu presentación.