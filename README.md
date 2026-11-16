# Presupuesto de la cena: balance energético diario para recomendar recetas

Proyecto del curso **INF3862 Plataformas Big Data para Data Science** (Magíster en Estadística - UC).
Autores: 
1. Joel Víctor Peña Carhuapoma
2. Sonia Curasma Quispe

## Caso de uso

Una app de recetas basada en Food.com recibe la actividad física de los relojes inteligentes de sus usuarios.
A las 18:00 (hora local), la app muestra a cada usuario **cuántas kilocalorías le quedan para la cena**
(gasto estimado del día − lo que ya comió) y le sugiere **cinco recetas de Food.com** que caben en ese margen.

- **Para quién:** usuarios con reloj vinculado (decidir qué cenar) y equipo de producto (balance y adherencia).
- **Datos:** wearable (dispositivos, mediciones, sesiones, comidas) + recetas y reseñas de Food.com.
- **Componente predictivo (E3):** estimar a las 18:00 el gasto calórico total del día, frente a una referencia trivial (promedio histórico del usuario).

## Entregas

| Entrega | Contenido | Estado |
|---|---|---|
| **E1 · Diseño de datos** | [Informe PDF](entregas/E1/informe.pdf) · [diagramas y notebook de perfilamiento](entregas/E1/anexos/) | Entregada el 16-11-2026 |
| E2 · Ingesta y procesamiento | Pipeline mínimo (notebook) sobre datos reales | Pendiente (30-11-2026) |
| E3 · Datos para ML y arquitectura final | Dataset de modelamiento, modelo base, arquitectura | Pendiente (14-12-2026) |

El registro de decisiones del proyecto está en [`decisiones.md`](decisiones.md).

## Estructura del repositorio

```
README.md              ← este archivo
decisiones.md          ← registro de decisiones (se actualiza en cada entrega)
entregas/
  E1/
    informe.pdf        ← informe de la Entrega 1 (3 páginas + anexos)
    anexos/            ← Figura1 (arquitectura), Figura2 (modelo OLTP entidad-relación), Figura3 (modelo OLAP estrella) y explorar_bases.ipynb
pyproject.toml         ← versión de Python y dependencias (uv)
uv.lock                ← versiones exactas, para reproducir el entorno
datos/
  README.md            ← cómo obtener los datos desde Canvas (no se suben al repositorio)
```

## Datos

Los datos los entrega el curso en Canvas y **no se suben** a este repositorio. Las instrucciones para obtenerlos y ubicarlos están en [`datos/README.md`](datos/README.md).

## Entorno y ejecución

La E1 no exige código. El notebook `entregas/E1/anexos/explorar_bases.ipynb` documenta el perfilamiento de
los datos (volúmenes y problemas citados en el informe) y, en su etapa 11, ejecuta las consultas C1–C7 del
Anexo D sobre una versión mínima de las tablas diseñadas. Se ejecuta en **JupyterLab**:

1. Descomprimir `foodcom.rar` y `wearable.rar` dentro de `datos/`, como indica [`datos/README.md`](datos/README.md).
2. Preparar el entorno con [uv](https://docs.astral.sh/uv/) y abrir JupyterLab desde la carpeta del proyecto:

   ```bash
   uv sync                  # crea .venv con las versiones exactas de uv.lock
   uv run jupyter lab       # abre JupyterLab
   ```

3. Abrir `entregas/E1/anexos/explorar_bases.ipynb` y ejecutar *Run → Run All Cells*.

## Hoja de ruta (coherencia entre entregas)

| Entrega | Qué se construye sobre la E1 |
|---|---|
| E2 | Notebook con DuckDB: cargar el crudo (bronce), aplicar reglas de calidad (duplicados, nulos, claves que no calzan, kcal extremas), escribir plata en Parquet particionado por día local, construir `fct_balance_diario` y `dim_usuario`, y ejecutar C4–C6. |
| E3 | Tabla de modelamiento usuario-día (la misma granularidad del hecho): objetivo = kcal gastadas del día; variables disponibles a las 18:00 (gasto y pasos hasta las 18:00, pasos de las últimas 3 h, promedio de los 7 días previos, tipo de día, modelo de reloj); separación temporal; referencia trivial = promedio histórico del usuario. |
