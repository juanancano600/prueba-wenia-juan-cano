# Prueba Técnica Operaciones – Juan Cano

Hola, este repositorio contiene mi solución para la prueba técnica de Operaciones. El objetivo fue automatizar la carga, análisis, comparación, georreferenciación y visualización de direcciones usando Python, AWS S3 y la API de Google Maps.

---

## ¿Qué hace este proyecto?

El flujo automatiza todo el proceso desde que tengo las direcciones, hasta que las muestro en un mapa interactivo. Explico el proceso paso a paso:

---

## Paso a paso

### 1. **Creación del archivo de direcciones**

No recibí un archivo original de direcciones, así que yo mismo generé `direcciones_originales.csv`. Este archivo es la base y contiene todas las direcciones que voy a procesar.

---

### 2. **Generación de variantes homónimas**

Para cada dirección original, programé una función que genera variantes de la misma dirección, por ejemplo:
- Cambio “CALLE” por “CLL”
- Cambio “CARRERA” por “CRA”
- Cambio “KRA” por “CRA”
- Y equivalentes para “NRO”, “NUM”, “NUMERO”

Estas variantes son posibles formas alternativas de escribir la misma dirección. Todas las variantes se guardan en el archivo `direcciones_homonimas.csv`.

---

### 3. **Comparación de variantes y filtrado por similitud**

Después, comparo la dirección original con sus variantes usando el algoritmo `token_sort_ratio` de fuzzywuzzy. Solo guardo las variantes que tengan más de 90% de similitud con la original, para asegurarme de quedarme solo con las verdaderamente homónimas.  
El resultado queda en `direcciones_similares.csv`.

---

### 4. **Carga de archivos a AWS S3**

Automatizo la carga de los archivos a la nube de AWS S3 usando Boto3. Para esto, debes poner tus credenciales reales en las variables:
```python
ACCESS_KEY = "AQUÍ_VA_TU_ACCESS_KEY"
SECRET_KEY = "AQUÍ_VA_TU_SECRET_KEY"
REGION = "us-east-2"  # o la región correspondiente
BUCKET = "prueba-tecnica-juan-cano"  # o el bucket que configures

---

### Pruebas unitarias 

Incluyo un archivo de pruebas unitarias (Pruebas.ipynb), donde valido las funciones principales del sistema, como la generación de variantes y la comparación de similitud.
Esto asegura que el código funciona correctamente y que los cambios futuros pueden ser probados fácilmente.