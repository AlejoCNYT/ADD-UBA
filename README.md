# TP Grupal — EDA Base de Películas IMDB

Trabajo práctico grupal de la materia **Análisis de Datos** (ADD). Análisis exploratorio
del dataset de películas IMDB (`movie.sqlite`).

## Contenido del repositorio

| Archivo | Descripción |
|---------|-------------|
| `EDA_movies.ipynb` | Notebook con el análisis exploratorio completo (carga, limpieza, estadística descriptiva, relaciones y visualizaciones). |
| `movie.sqlite` | Base de datos con 3 tablas relacionadas por `Movie_id`: `IMDB` (117 filas), `earning` (117 filas) y `genre` (351 filas). |
| `slide_1.jpg`, `slide_2.jpg`, `slide_3.jpg` | Diapositivas resumen del análisis. |
| `TP_Grupal_slides.pptx` | Presentación editable (importable a Google Slides). |

## Cómo ejecutar el notebook

```bash
pip install jupyter pandas numpy matplotlib seaborn scipy
jupyter notebook EDA_movies.ipynb
```

El archivo `movie.sqlite` debe estar en la misma carpeta que el notebook.

## Autores

- Mariano Marchetta
- Daniel Alejandro Acero Varela
