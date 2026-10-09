# Tablero de indicadores · Comunicaciones FCV

Tablero en línea que grafica, mes a mes, los indicadores de la pestaña **Comunicaciones**
del archivo *INDICADORES ÁREAS FCV 2026.xlsx*, para reportar a la dirección ejecutiva.

## Qué muestra

- **Resumen del mes** (selector arriba a la derecha): fichas con semáforo y una
  "Lectura para dirección ejecutiva" redactada automáticamente a partir de los datos.
- **Comunicaciones externas** (iniciativa 3):
  - Visitas únicas a los sitios FCV y FCV Oficios, con la línea de meta (+10% sobre la base).
  - Engagement por red (Instagram, Facebook y LinkedIn FCV; Facebook Oficios) con la
    franja del rango esperado.
  - Menciones en medios externos, con meta mensual y acumulado.
- **Matriz de cumplimiento** indicador × mes (cumple / en camino / bajo meta / revisar / sin registro).
- **Comunicaciones internas** (iniciativas 1 y 2): metas de las encuestas semestrales y post evento,
  marcadas como pendientes mientras la planilla no tenga resultados.

## Cómo actualizarlo cada mes

Opción A — sin programar: abre el tablero, pulsa **Cargar Excel actualizado** (o arrastra el
archivo) y elige el .xlsx descargado desde Drive. El archivo se lee solo en el navegador.

Opción B — dejar la copia actualizada en el repositorio:

```bash
pip install openpyxl
python3 scripts/actualizar_datos.py "INDICADORES ÁREAS FCV 2026.xlsx"
git commit -am "Datos de comunicaciones: <mes>" && git push
```

Opción C — conexión en línea permanente: convierte el archivo a Hoja de cálculo de Google,
publica la pestaña Comunicaciones como CSV (*Archivo › Compartir › Publicar en la web*) y pega
esa URL en `CONFIG.urlCsv` dentro de `index.html`. El tablero alojado en GitHub Pages leerá la
planilla cada vez que se abra.

## Cómo se leen las celdas

La planilla usa texto libre; el tablero lo interpreta así (conviene mantener el formato):

| Indicador | Formato esperado en la celda |
|---|---|
| Visitas únicas | `FCV: 3.540 FCV Oficios: 3.042` |
| Engagement | `FCV: IG: 8,01% FB: 3,2% LK: 3,5% Oficios: FB: 0,93%` (todo lo que va después de "Oficios" se asigna a FCV Oficios) |
| Menciones | un número |

Supuestos ajustables en `CONFIG` (al inicio del script de `index.html`):

- **Base de la meta web**: por defecto, el primer mes con datos (enero 2026). Si existe el
  promedio 2025, conviene usarlo (`baseWeb`).
- **Rangos de engagement**: tomados de la columna Meta de la planilla.
- Valores de engagement sobre 100% (Facebook FCV jun–ago) se marcan **Revisar dato** y no se grafican.

## Publicar en GitHub Pages

*Settings › Pages › Deploy from a branch* y elegir la rama con `index.html` en la raíz.
