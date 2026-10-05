# Instrucciones de etiquetado de recortes de arándanos

Este documento explica cómo llenar el archivo `Datos/resultados_avance1/etiquetas.csv`, que contiene **una fila por recorte** (439 en la corrida actual). Cuando esté lleno, la libreta `Notebooks/Avance1.Equipo6.ipynb` lo lee automáticamente y activa el análisis supervisado (balance de clases, relevancia de características, boxplots por clase).

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `Datos/resultados_avance1/etiquetas.csv` | **Archivo a llenar.** Viene con las columnas `clase`, `defecto` y `notas` vacías. |
| `Datos/resultados_avance1/etiquetas_ejemplo.csv` | Cuatro filas de ejemplo (un bueno, dos malos y un fragmento). **No lo lee la libreta**: es solo referencia. |
| `Datos/recortes_locales/` | Los recortes de 200×200 que se están etiquetando (se generan al ejecutar la libreta; **no se suben al repositorio**). |

## Qué se llena

| Columna | Qué poner | Obligatoria |
|---|---|---|
| `crop_id` | **No se toca.** Es la llave que une la fila con la imagen (`<foto>_blueberry_<n>`). | — |
| `foto`, `cx`, `cy`, `radio` | **No se tocan.** Origen y posición del recorte en la foto. | — |
| `clase` | Solo `bueno` o `malo`, en minúsculas. Déjela vacía si no es un fruto completo o si hay duda. | Sí |
| `defecto` | Defecto principal, con uno de los nombres de la tabla siguiente, escrito siempre igual. | Solo si es `malo` |
| `notas` | Texto libre (por ejemplo, «ver con SOLID»). | No |

## Defectos principales

Los nombres salen de la Tabla 8 del Avance 0. Úsenlos tal cual:

| `defecto` | Cómo se ve | `clase` |
|---|---|---|
| `ninguno` | Fruto completo, piel azul oscura uniforme, con pruina (capa blanquecina), firme y sin marcas | bueno |
| `coloracion_anormal` | Zonas rojizas o moradas en la piel | malo |
| `golpe` | Zona hundida o aplastada, a veces más oscura | malo |
| `cicatriz` | Marca o raspadura clara sobre la piel | malo |
| `deshidratado` | Piel arrugada | malo |
| `descompuesto` | Zonas blandas, húmedas, con moho o muy oscuras | malo |
| `inmaduro` | Verde o rojo claro | malo |
| `flor_seca` | Restos secos de la flor pegados al fruto | malo |

> **Importante.** Las descripciones son orientativas. El criterio real de qué es «malo» lo define **SOLID México**. Antes de etiquetar todo, acuerden con ellos unos cinco ejemplos por defecto y apliquen la misma regla a todos los recortes.

## Ejemplo

```csv
crop_id,foto,cx,cy,radio,clase,defecto,notas
IMG_1369_HEIC_enhanced_blueberry_001,IMG_1369_HEIC_enhanced,1431.6,2126.8,380,bueno,ninguno,
IMG_1370_HEIC_enhanced_blueberry_001,IMG_1370_HEIC_enhanced,1511.5,2325.8,559,malo,cicatriz,marca clara cerca del cáliz
IMG_1371_HEIC_enhanced_blueberry_001,IMG_1371_HEIC_enhanced,1926.5,1460.0,544,malo,golpe,zona hundida
IMG_1372_HEIC_enhanced_blueberry_002,IMG_1372_HEIC_enhanced,980.2,1105.7,52,,,fragmento del fruto no completo
```

Las clases y defectos de este ejemplo son **ilustrativos**: no corresponden a una revisión real de esos recortes.

## Casos especiales

- **Varios defectos en un mismo fruto:** ponga el principal en `defecto` y el resto en `notas`. Si pone varios en `defecto`, sepárelos con `;`. La libreta hoy no los separa, así que se contarán como una categoría distinta.
- **Fragmentos:** hay unos 24 recortes de radio muy pequeño (menor a la mitad de la mediana). Son pedazos de fruto o reflejos, no frutos completos. Déjelos **sin `clase`**; la libreta los excluye de todos modos.
- **Dudas:** deje `clase` vacía y explique en `notas`. Es mejor dejar un recorte sin etiquetar que etiquetarlo mal.
- **No cambie `crop_id` ni borre filas.** La libreta une por `crop_id`; si no coincide, la etiqueta se pierde.

## Cómo trabajar

1. Abra la carpeta `Datos/recortes_locales/` (ordenada por nombre) y el CSV al mismo tiempo.
2. Llene primero `clase`. Después llene `defecto` solo para los recortes `malo`.
3. **Dos personas** deben etiquetar una muestra común de unos 30 recortes y comparar. Si no coinciden, ajusten el criterio antes de continuar; eso mide qué tan subjetivo es el etiquetado.
4. Guarde el archivo como **CSV UTF-8** con el mismo nombre (`etiquetas.csv`) en `Datos/resultados_avance1/`. En Excel: *Guardar como → CSV UTF-8 (delimitado por comas)*.

## Cómo comprobar que quedó bien

Ejecute la libreta `Avance1.Equipo6.ipynb`. En la sección 3.7 debe aparecer:

```
Etiquetas leídas de etiquetas.csv: N recortes etiquetados
```

y se ejecutará el bloque supervisado (conteo y porcentaje por clase, razón de desbalance, pesos de clase y relevancia de características). Si aparece «No existe etiquetas.csv» o N = 0, revise el nombre, la ubicación y que `clase` solo contenga `bueno` o `malo`.

## Confidencialidad

El archivo de etiquetas solo contiene identificadores, coordenadas y la clase asignada, y puede versionarse. Las **imágenes** de SOLID México no deben subirse al repositorio: están excluidas por `.gitignore` (`Datos/Semana3/`, `Datos/recortes_locales/`, `Datos/muestras/`).
