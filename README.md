# Extractor De Audio Y Video Para Contenido Autorizado

## Origen De Esta Necesidad

Este proyecto nació por una necesidad concreta: organizar y preparar contenido audiovisual para un evento próximo, evitando el uso de sitios de terceros que prometen conversiones rápidas pero que pueden exponer al usuario a publicidad agresiva, redirecciones sospechosas o archivos no confiables.

Además, este proyecto fue desarrollado desde cero como parte de un proceso de aprendizaje práctico en el uso de agentes de IA. La implementación se construyó con apoyo de CODEX y GPT-5.4, tomando una idea inicial y transformándola en una herramienta funcional, controlada y personalizable.

## Aviso Importante

Esta herramienta es solo para contenido sin copyright o con permiso del autor.

Su uso está pensado con fines educativos, de automatización personal y de gestión de contenido propio, con licencia o con autorización expresa.

## Que Hace Este Proyecto

Este proyecto permite procesar URLs compatibles mediante Python para:

- descargar un archivo de video
- extraer un archivo de audio MP3 a partir del video
- guardar los archivos fuera del workspace de scripts
- actualizar una lista en texto
- actualizar un catalogo en JSON
- detectar duplicados exactos y similitudes por nombre

## Inicio Rapido

### Requisitos

Antes de usar este proyecto necesitas tener instalado:

- Python 3
- `pip` para instalar dependencias de Python
- `ffmpeg`
- `node`

Notas:

- El proyecto fue probado con Python `3.14.3`
- `ffmpeg` se usa para convertir el video a MP3
- `node` se usa como apoyo para `yt-dlp` al resolver ciertos retos tecnicos de extracción

### Instalar Dependencias

Desde la carpeta del proyecto ejecuta:

```powershell
py -m pip install -r requirements.txt
py -m pip install -U "yt-dlp[default]"
```

### Cambiar La Carpeta De Descarga

Por defecto las descargas se guardan en:

```text
C:\Musica_Boda
```

Si deseas usar otra carpeta, cambia esta linea en:

- el archivo `media_downloader.py`, que se encuentra en la carpeta donde descargaste o clonaste este proyecto

```python
DEFAULT_OUTPUT_DIR = Path(r"C:\Musica_Boda")
```

### Ejecutar El Script

Para iniciar el script interactivo ejecuta:

```powershell
py media_downloader.py
```

Luego el script:

- pedira una URL compatible
- descargara el video
- generara el MP3
- actualizara `lista.txt`
- actualizara `catalogo.json`
- permitira salir escribiendo `s`

### Si YouTube Pide Verificacion O Cookies

Algunas URLs de YouTube pueden devolver mensajes como:

- `Sign in to confirm you're not a bot`

Esto puede pasar por cambios recientes de YouTube en sus controles de acceso y anti-bot. Cuando ocurra, el proyecto puede necesitar cookies validas de una sesion iniciada.

En ese caso, reintenta importando cookies desde tu navegador:

```powershell
py media_downloader.py --cookies-from-browser edge
```

Tambien puedes usar otros navegadores compatibles:

- `chrome`
- `brave`
- `firefox`

Si ya exportaste un archivo de cookies en formato Netscape, puedes usar:

```powershell
py media_downloader.py --cookies-file "C:\ruta\cookies.txt"
```

Nota:

- el navegador elegido debe tener una sesion valida iniciada para YouTube
- si aun asi falla, vuelve a exportar cookies frescas o prueba otra URL

### Uso Recomendado Con `cookies.txt`

En Windows, si `yt-dlp` no logra leer directamente la base de cookies de Chrome, la forma mas estable es exportarlas manualmente a un archivo `cookies.txt` en formato Netscape.

Pasos recomendados:

1. Inicia sesion en YouTube desde Chrome.
2. Abre `youtube.com`.
3. Exporta las cookies en formato Netscape con tu extension.
4. Guarda o pega el contenido en un archivo llamado `cookies.txt`.
5. Coloca ese archivo en la misma carpeta que `media_downloader.py`.

Si `cookies.txt` existe junto al script, el proyecto lo detecta automaticamente al iniciar. En ese caso, puedes seguir ejecutando solo:

```powershell
py media_downloader.py
```

Notas importantes:

- no conviene versionar ni compartir `cookies.txt`, porque contiene datos sensibles de sesion
- si vuelve a aparecer un error de autenticacion, normalmente basta con exportar un `cookies.txt` nuevo y reemplazar el anterior
- no hay un tiempo fijo de validez; puede durar dias o semanas segun YouTube y el estado de tu sesion

## Libreria Utilizada

La libreria principal utilizada es:

- `yt-dlp`

Repositorio oficial:

- [https://github.com/yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp)

Adicionalmente el proyecto usa:

- `ffmpeg` para convertir el video descargado a MP3
- `node` como runtime JavaScript de apoyo para `yt-dlp`
- `yt-dlp[default]` / `yt-dlp-ejs` para mejorar compatibilidad tecnica

## Estructura De Salida

Las descargas no se guardan en la carpeta donde estan estos scripts.

Actualmente se guardan en un directorio externo:

- `C:\Musica_Boda`

Dentro de esa ruta se usan estas carpetas y archivos:

- `C:\Musica_Boda\video`
- `C:\Musica_Boda\audio`
- `C:\Musica_Boda\lista.txt`
- `C:\Musica_Boda\catalogo.json`

## Que Se Actualiza En Cada Descarga

Cuando una descarga termina correctamente:

- se guarda el video en `video`
- se genera el MP3 en `audio`
- se actualiza `lista.txt`
- se actualiza `catalogo.json`

`lista.txt`:

- guarda una lista enumerada de elementos procesados
- el formato actual usa 3 digitos: `001`, `002`, `003`, etc.

`catalogo.json`:

- guarda informacion estructurada de cada descarga
- incluye `id`, `title`, `webpage_url`, `video_file`, `audio_file`, `downloaded_at`

## Duplicados Y Similitud

El script intenta evitar descargas repetidas de dos maneras:

- compara por un identificador unico del contenido si el archivo ya fue descargado
- compara por similitud de titulo si encuentra nombres parecidos

Si detecta una similitud:

- muestra el titulo del contenido que se intenta descargar
- muestra coincidencias parecidas encontradas en la lista
- le pregunta al usuario si desea continuar o no

## Manejo De Descargas Incompletas

Si una descarga falla:

- se muestra un mensaje de error en rojo
- se eliminan los archivos `.part` relacionados con esa descarga inconclusa

Eso evita dejar archivos temporales que despues confundan la carpeta `video`.

## Archivo Principal

El script principal es:

- `media_downloader.py`

Tambien existe este auxiliar:

- `generate_song_list.py`

## Cambiar El Directorio De Descarga

La ruta por defecto se define en el codigo fuente dentro de:

- `media_downloader.py`

Buscando esta linea:

```python
DEFAULT_OUTPUT_DIR = Path(r"C:\Musica_Boda")
```

Actualmente esa definicion esta en:

- `media_downloader.py`, linea 14

Si se desea usar otra carpeta, se puede cambiar esa linea por otra ruta.

## Como Ejecutarlo

Ejecutar el script principal:

```powershell
py media_downloader.py
```

El script:

- pide una URL compatible
- permite salir escribiendo `s`
- descarga video y audio
- actualiza `lista.txt` y `catalogo.json`

## Continuidad Con Otro Agente

Si este proyecto se va a continuar con otro agente, ya existe un archivo de estado con el contexto tecnico y decisiones tomadas:

- `PROJECT_STATUS.md`

Ese archivo resume:

- lo que ya se hizo
- decisiones tecnicas tomadas
- dependencias instaladas
- flujo del script
- recomendaciones para continuar el desarrollo
