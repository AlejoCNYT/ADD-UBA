# 📊 Análisis Exploratorio de Datos (EDA) - Base de Películas IMDB

## 📌 Descripción

Análisis exploratorio completo del dataset de películas IMDB (`movie.sqlite`). 
Este notebook incluye carga de datos, limpieza, estadística descriptiva, análisis de correlaciones y visualizaciones avanzadas para identificar patrones en la industria cinematográfica.

**Conclusión clave:** El dinero genera dinero, pero NO calidad. La industria es altamente desigual.

---

## 📂 Estructura del Dataset

El archivo `movie.sqlite` contiene **3 tablas relacionadas** por `Movie_id`:

| Tabla | Filas | Descripción |
|-------|-------|-------------|
| **IMDB** | 117 | Información de películas: rating, votos, MetaCritic, presupuesto, duración, votos por demografía |
| **earning** | 117 | Recaudación: Domestic y Worldwide |
| **genre** | 351 | Géneros (relación 1-a-muchos, 21 géneros únicos) |

**Variables totales:** 54 columnas

---

## 📊 Contenido del Análisis

### 1️⃣ **Carga e Inspección**
- Conexión a SQLite
- Lectura de las 3 tablas
- Shape y estructura inicial

### 2️⃣ **Limpieza de Datos**
- Conversión de variables (Runtime, MetaCritic, Budget de texto a numérico)
- Tratamiento de valores faltantes
- Merge de tablas por Movie_id

**Valores faltantes encontrados:**
- MetaCritic: 7 nulos
- Budget: 3 nulos
- Runtime: 21 nulos
- Géneros vacíos: 41 registros

### 3️⃣ **Estadística Descriptiva**
- Medidas de tendencia central (media, mediana)
- Medidas de dispersión (desvío, rango)
- Cuartiles y percentiles
- Variables analizadas: Rating, Budget, Worldwide, MetaCritic, Runtime

**Insights clave:**
- Rating promedio: **7.9** (concentrado entre 7.6-8.0)
- Rango muy estrecho en ratings (mayoría "prestigiosas")
- Presupuestos: $10M - $100M (la mayoría)
- Recaudaciones: extremadamente variable (outliers significativos)

### 4️⃣ **Variables Categóricas: Géneros**
- **Drama:** 77 películas (género dominante)
- **Adventure:** segundo más frecuente
- **Action:** tercero

**Conclusión:** El género tiene POCO poder explicativo sobre la calidad/recaudación

### 5️⃣ **Correlaciones**

**Matriz de correlaciones:**

| Variables | Correlación | Interpretación |
|-----------|-------------|-----------------|
| Budget ↔ Worldwide | **0.86** | ✅ Fuerte positiva |
| Worldwide ↔ Domestic | **0.96** | ✅ Muy fuerte positiva |
| Rating ↔ Worldwide | **-0.08** | ❌ Sin relación |
| Budget ↔ Rating | **-0.15** | ❌ Débil negativa |
| Rating ↔ TotalVotes | **0.63** | ✅ Moderada positiva |
| MetaCritic ↔ Worldwide | **-0.25** | ❌ Relación inversa |

**Conclusiones:**
- ✅ Si inviertes MÁS dinero → GANAS más dinero
- ❌ Si inviertes MÁS dinero → NO recibes mejor calificación
- ❌ Si GANAS más dinero → NO es necesariamente mejor película
- ✅ Si es MÁS POPULAR → recibe mejor calificación
- ❌ Las películas MÁS LARGAS NO son mejor calificadas
- ❌ Los críticos profesionales y el público NO coinciden

### 6️⃣ **Análisis de Distribuciones**

**Distribuciones Normales (similitud entre películas):**
- Rating: normal, concentrado 7.6-8.0
- Runtime: normal, 100-130 minutos
- MetaCritic: normal
- Budget: normal (10M-100M)

**Distribuciones Sesgadas (desigualdad extrema):**
- **Worldwide:** ALTAMENTE sesgada con outliers (2-3 blockbusters dominan)
- **TotalVotes:** sesgada con cola larga

### 7️⃣ **Escala Logarítmica (Análisis Económico)**

**¿Por qué escala logarítmica?**
Los valores económicos varían exponencialmente (de $1M a $1.000M). 
La escala logarítmica permite ver todos los valores en el mismo gráfico.

**Hallazgos clave:**
- **Budget (log):** La mayoría de películas cuestan similar ($10M-$100M) → distribución casi normal
- **Worldwide (log):** Incluso en escala logarítmica, hay 2-3 películas que ganan MUCHÍSIMO más
  
**Conclusión:** Los outliers NO son un artefacto visual, sino una característica REAL de la industria:
```
🎬 Avatar, Avengers Endgame, Star Wars: The Force Awakens
   dominan completamente las ganancias mundiales
```

---

## 🎯 Películas Destacadas

| Métrica | Película | Valor |
|---------|----------|-------|
| **Más votada** | Inception (2010) | 2.5M+ votos |
| **Mayor recaudación** | Star Wars: The Force Awakens (2015) | $2.0B+ |
| **Rating promedio del dataset** | - | 7.9 |
| **Género más común** | Drama | 77 películas |

---

## 💡 Conclusiones Principales

### 1. **El dinero genera dinero, pero NO calidad**
```
Correlación Budget-Rating: -0.15 (prácticamente nula)
Correlación Budget-Worldwide: 0.86 (muy fuerte)

→ Gastar más presupuesto te ayuda a ganar más dinero,
  pero NO a hacer películas mejor calificadas
```

### 2. **La industria es altamente desigual**
```
Budget: casi uniforme (mayoría 10M-100M)
Worldwide: extremamente concentrada (pocos blockbusters capturan 80% del dinero)

→ Miles de películas luchan por presupuestos similares,
  pero solo un puñado gana de verdad
```

### 3. **Los críticos y el público NO coinciden**
```
Correlación MetaCritic-Worldwide: -0.25 (inversa!)

→ Películas muy bien calificadas por críticos 
  ganan MENOS dinero que las menos críticas
```

### 4. **La popularidad determina la calidad percibida**
```
Correlación Rating-TotalVotes: 0.63 (moderada)

→ Las películas con muchos votos reciben mejor rating
  (efecto "rebaño" o selección: películas populares = mejor puntuadas)
```

### 5. **El género es poco importante**
```
Drama domina, pero hay poca diferencia de quality/recaudación 
entre géneros

→ El éxito no depende del género, sino de otros factores
  (presupuesto, marketing, actores, timing)
```

---

## 🛠️ Requisitos y Dependencias

```python
import sqlite3
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

**Archivo requerido:** `movie.sqlite` (debe estar en la misma carpeta)

---

## 📈 Visualizaciones Incluidas

1. **Histograma de Rating:** Distribución concentrada 7.6-8.0
2. **Barplot de Géneros:** Drama domina con 77 películas
3. **Scatter Plot (log):** Budget vs Worldwide con color por Rating
4. **Heatmap de Correlaciones:** Matriz completa de relaciones
5. **Boxplots de Distribuciones:** Budget y Worldwide en escala logarítmica
6. **Distribution Plots:** Histogramas + KDE de todas las variables

---

## 📊 Estadísticas Clave Resumidas

```
Total de películas: 117
Columnas totales: 54
Variables numéricas: 7
Géneros únicos: 20

Rating promedio: 7.9
Rating rango: 6.2 - 8.9

Budget promedio: ~$60M
Worldwide promedio: ~$350M

Películas con MetaCritic completo: 110 (7 nulos)
Películas con Budget completo: 114 (3 nulos)
Películas con Runtime completo: 96 (21 nulos)
```

---

## 🚀 Cómo Usar Este Notebook

1. **Descargar** `movie.sqlite` en la misma carpeta que el notebook
2. **Ejecutar** todas las celdas en orden
3. **Interpretar** los gráficos y tablas
4. **Usar los insights** como base para las diapositivas del TP grupal

---

## 👥 Autores

- **Mariano Marchetta**
- **Daniel Alejandro Acero Varela**

Dataset: Full TMDB Movies Dataset 2024

---

## 📝 Notas Importantes

- El dataset contiene solo películas "prestigiosas" (ratings 6.2-8.9)
- Los outliers en recaudación son REALES, no artefactos visuales
- La escala logarítmica es esencial para visualizar datos económicos
- Las correlaciones revelan dinámicas ocultas (críticos vs público)

---

## 📌 Para las Diapositivas

**Use estos puntos clave:**

✅ Dinero → Dinero, pero NO Calidad
✅ Presupuestos uniformes, ganancias concentradas
✅ Críticos ≠ Público (correlación inversa!)
✅ Popularidad > Calidad (efecto rebaño)
✅ Género = poco importante
✅ Solo 2-3 películas dominan las ganancias mundiales

```

---
**Copiar TODO lo de arriba (desde `# 📊` hasta el último `)**, ir a GitHub, crear nuevo archivo `README.md` en tu rama, pegar y commit.**

¿Listo para hacer el PR? 🚀
