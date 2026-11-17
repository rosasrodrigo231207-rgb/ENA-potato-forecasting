# Artículo ICALTER 2026 — Pronóstico del rendimiento de papa (ENA 2015–2025)

**Título:** *Time Series Forecasting with a Pretrained AI Model for Teaching: Potato Yield from Peru's National Agricultural Survey (2015–2025)*

**Título en español:** *Pronóstico de series de tiempo con un modelo de IA preentrenado para la enseñanza: rendimiento de papa de la Encuesta Nacional Agropecuaria del Perú (2015–2025)*

**Autores:** Rodrigo Claudio Rosas Tuni, Fred Torres Cruz, David León Callohuanca Condori y Yonhel Mamani Cruz. Ingeniería Estadística e Informática, Universidad Nacional del Altiplano, Puno.

**Congreso:** ICALTER 2026 · Track 2: *Emerging Technologies in Education* · IEEE, en inglés, de 4 a 6 páginas, en PDF · se envía por EasyChair: https://easychair.org/conferences/?conf=icalter2026

---

## Contenido del paquete

| Carpeta | Archivo | Qué es |
|---|---|---|
| raíz | `Articulo_ICALTER2026_EN.pdf` | **El artículo para enviar** (inglés, plantilla IEEE conference, A4, 5 páginas) |
| raíz | `Articulo_ICALTER2026_ES.pdf` | Versión en español, para estudiar y preparar la exposición (no se envía) |
| `articulo/` | `main.tex` (inglés) y `main_es.tex` (español), con sus partes (`abstract`, `body`, `results`, `discussion`, `conclusions`), `references.tex`, `numbers*.tex`, `tab_*.tex`, `fig*.pdf`, `IEEEtran.cls` | El código LaTeX editable. En Overleaf, compilen `main.tex` para el inglés o `main_es.tex` para el español |
| `notebook/` | `ENA_papa_pronostico_Colab.ipynb` | El recurso didáctico: notebook interactivo de Google Colab, en español |
| `codigo/` | `ena_forecast.py` | Funciones de los modelos (Ingenuo, ARIMA, ETS, Chronos-2), la validación y las métricas |
| `codigo/` | `make_paper_assets.py` | Regenera las figuras, las tablas y las cifras del artículo a partir de los pronósticos |
| `codigo/` | `ena_series_etapas.py` | Su script original que procesa los microdatos de la ENA (.sav de 3,8 millones de filas) |
| `datos/` | `series_ENA_papa.xlsx`, `rendimiento_papa_ENA_2015_2025.csv` | Series de rendimiento: la nacional y las de 19 departamentos |
| `resultados/` | `pronosticos_todos_los_modelos.csv`, `metricas.csv` | Los pronósticos de su ejecución en Colab (con Chronos-2) y sus métricas (MAE, MAPE, MASE, MSIS y cobertura). Todas las cifras del artículo salen de estos archivos |
| `taller/` | `Guia_taller.pdf` | Guía del taller de 60 minutos (para el estudiante y el docente) |
| `taller/` | `crear_formulario_TAM.gs` | Script que crea solo el cuestionario TAM en Google Forms |
| `taller/` | `analisis_TAM.py` | Calcula el alfa de Cronbach y las medias cuando tengan respuestas |

---

## Antes de enviar (checklist)

1. **Correos y ORCID:** ya están todos en el PDF: Rodrigo (rodrigorosas@est.unap.edu.pe, ORCID 0009-0007-9108-7525), Fred Torres Cruz (ftorres@unap.edu.pe, ORCID 0000-0003-0834-6834), David (davidcallohuanca@est.unap.edu.pe, ORCID 0009-0006-1454-4828) y Yonhel (72689624@est.unap.edu.pe, ORCID 0009-0003-2171-0183). Usen esos mismos correos en EasyChair.
2. **Autores:** son 4 (el máximo es 6). En EasyChair agréguenlos en el mismo orden del PDF.
3. **GitHub:** creen el repositorio público `ENA-potato-forecasting` en la cuenta `rosasrodrigo231207-rgb` y suban las carpetas `notebook/`, `codigo/`, `datos/`, `resultados/` y `taller/`. El artículo ya cita esa dirección.
4. **Compilar (solo si cambian algo):** en https://www.overleaf.com usen *New Project → Upload Project* con la carpeta `articulo/` en ZIP, y luego *Recompile → Download PDF*.
5. **Enviar:** EasyChair → *New Submission* → Track 2 → suban `Articulo_ICALTER2026_EN.pdf`, más el título, el resumen y las palabras clave (están en el PDF).
6. **Fechas:** última convocatoria el 16 de noviembre, notificación el 24 de noviembre, versión final y registro el 30 de noviembre, y exposición oral el 10 u 11 de diciembre en Moquegua (modalidad híbrida).

## Cómo usar el notebook

Abran https://colab.research.google.com y vayan a *Archivo → Subir notebook*. Luego usen *Entorno de ejecución → Ejecutar todo*. No necesita GPU. Al final se descargan los dos CSV de resultados.

## Cómo crear el cuestionario TAM

Entren a https://script.google.com y creen un nuevo proyecto. Peguen `taller/crear_formulario_TAM.gs` y ejecuten `crearFormularioTAM`. En el registro aparece el enlace del formulario.

## Resultados principales (para la exposición)

- Con solo 7 años de entrenamiento, ARIMA se volvió la media histórica en 19 de las 20 series, y ETS se comportó como la media o como el último valor.
- Chronos-2 tuvo el menor MAPE medio (16,9 % en el holdout y 15,5 % en la ventana expansiva) y casi nunca fue el peor modelo, aunque solo ganó en 3 series.
- Con el MASE (error escalado) todos los modelos quedan entre 1,23 y 1,33: ninguno supera al error ingenuo dentro de la muestra.
- Con el MSIS (calidad del intervalo), Chronos-2 fue el mejor en el holdout (5,33).
- Ninguna diferencia entre modelos fue significativa (Friedman p ≥ 0,09 en MAPE, MASE y MSIS).
- Los intervalos del 80 % de ARIMA y ETS fallan mucho (aciertan cerca del 60 %). Los de Chronos-2 acertaron el 80 % en el holdout.
- En Puno, la helada de 2023 explica los errores grandes.

Si vuelven a correr el notebook con otra versión de las librerías, ETS y ARIMA pueden dar diferencias menores al 0,3 %. Es normal.

## Para la exposición: limitaciones que deben saber explicar

- **Pocos datos:** solo hay 4 años de prueba por serie. Por eso las diferencias entre modelos no son significativas según la prueba de Friedman.
- **Año 2020:** está interpolado porque no hubo ENA. Es una estimación, no un dato.
- **Cambios de muestra:** el número de registros de papa sube mucho en 2023–2025. Por eso se modela el rendimiento, que es una razón, y no la producción.
- **Superficie imputada:** en 2015 y 2018 la superficie se convirtió de unidades locales a hectáreas.
- **Evaluación educativa:** el taller y el TAM se presentan como protocolo. Su aplicación queda como trabajo futuro.
