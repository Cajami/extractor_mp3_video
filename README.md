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
pip install -r requirements.txt
python -m pip install -U "yt-dlp[default]"
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
python media_downloader.py
```

Luego el script:

- pedira una URL compatible
- descargara el video
- generara el MP3
- actualizara `lista.txt`
- actualizara `catalogo.json`
- permitira salir escribiendo `s`

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
python media_downloader.py
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
