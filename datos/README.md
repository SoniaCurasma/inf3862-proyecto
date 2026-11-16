# Datos del proyecto: Presupuesto de la cena

Archivos utilizados:

| Fuente | Archivos | Origen |
|------------------------|------------------------|------------------------|
| Recetas (Food.com) | `recipes.parquet` (en `foodcom.rar`) | Canvas · Kaggle "Food.com - Recipes and Reviews" (CC0) |
| Reseñas (Food.com) | `reviews.parquet` (en `foodcom.rar`) | Canvas |
| Wearable | `dispositivos.csv`, `mediciones/AAAA-MM-DD/HH.jsonl.gz`, `sesiones.jsonl`, `comidas.csv`, `LEEME.md` | Canvas, archivo `wearable.rar` (datos sintéticos del curso) |

## Cómo ubicarlos:

Debe quedar así:

```         
datos/
  README.md
  foodcom/
    recipes.parquet
    reviews.parquet
  wearable/
    LEEME.md
    dispositivos.csv
    comidas.csv
    sesiones.jsonl
    mediciones/
      2007-12-16/05.jsonl.gz … 23.jsonl.gz   (el primer día empieza a las 05 UTC)
      …  (61 carpetas, una por día de recepción; 1.449 archivos)
```

## Volumen de referencia

| Archivo                      | Filas      | Tamaño                          |
|------------------------|------------------------|------------------------|
| recipes.parquet              | 522.517    | 179 MB                          |
| reviews.parquet              | 1.401.982  | 174 MB                          |
| mediciones/ (1.449 archivos) | 15.540.132 | 116 MB comprimido · 2,2 GB JSON |
| sesiones.jsonl               | 4.840      | 0,8 MB                          |
| comidas.csv                  | 22.106     | 1,0 MB                          |
| dispositivos.csv             | 315        | 20 KB                           |
