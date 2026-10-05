# Datos

Imágenes de arándanos entregadas por **SOLID México** para el proyecto Berry-Vision. Se publican con su autorización.

## Qué contiene este repositorio

| Ruta | Contenido |
|---|---|
| [`Semana3/output/`](Semana3/output) | **251 recortes individuales** de arándanos (PNG cuadrados, de 456 a 1256 px de lado), de la corrida inicial del extractor. Corresponden a las fotos IMG_1396 a IMG_1528. |
| [`Semana3/etiquetas.csv`](Semana3/etiquetas.csv) | **Etiquetas** de 439 recortes (de las fotos IMG_1369 a IMG_1530): `clase` (`bueno`/`malo`), `defecto` y `notas`. 243 buenos, 177 malos y 19 sin clasificar. |
| [`muestras/muestra_01.jpg`](muestras/muestra_01.jpg) | Fotografía de la banda con muchos arándanos a la vez (vista de la máquina). |
| [`resultados_avance1/`](resultados_avance1) | Tablas agregadas generadas por la libreta (manifiestos y plantilla de etiquetado). |

## Qué NO está en el repositorio (permanece en Drive del equipo)

- Las **fotos originales** (`image/`): 161 PNG de 12 MP (4032×3024), unos 1.2 GB.
- Las imágenes con los **límites detectados** (`Bondary/`): se regeneran con el extractor.
- Los **recortes regenerados** a 200×200 que usa el modelo (480 en la última corrida): se generan al ejecutar la libreta.

> **Aviso.** `Semana3/output/` es una copia de la corrida inicial: tiene 251 recortes, mientras que la versión más reciente del dataset en Drive tiene 463 en `output/` y la libreta regenera 480 recortes de 161 fotos. Los identificadores de `etiquetas.csv` (`<foto>_blueberry_<n>`) son los de los recortes que regenera la libreta, no necesariamente los de `output/`. Este archivo cubre 439 recortes de 146 fotos (IMG_1369 a IMG_1530); la ejecución en Colab usó 161 fotos y 480 recortes, de los cuales 410 quedaron etiquetados tras el control de calidad.

## Estructura de los datos

- **Fotos originales:** PNG a color, 4032×3024 px (159 horizontales y 2 verticales), con 1 a 5 arándanos cada una sobre fondo gris claro.
- **Recortes:** cuadrados centrados en cada fruto (radio detectado + 20 px de relleno), de tamaño variable; la libreta los reduce a 200×200 con `INTER_AREA`.
- **Etiquetas:** `clase` (`bueno` / `malo`) y `defecto` (`ninguno`, `cicatriz`, `flor_seca`, `deshidratado`, `coloracion_anormal`, `golpe`, `descompuesto`, `inmaduro`).

## Cómo reproducir el análisis

La libreta [`Notebooks/Avance1.Equipo6.ipynb`](../Notebooks/Avance1.Equipo6.ipynb) se ejecutó en Google Colab leyendo la carpeta compartida del equipo en Drive. Para ejecutarla en otro entorno, apunte `BERRY_DATA_DIR` a una carpeta con `image/`, `output/` y `Bondary/` (y `etiquetas.csv` junto a ellas para el análisis supervisado; la libreta lo busca primero en esa carpeta).
