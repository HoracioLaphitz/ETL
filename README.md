# ETL — PIB Mundial (Extracción, Transformación y Carga)

Script de Python que ejecuta un proceso ETL completo sobre la lista de países por PIB nominal, tomando como fuente una captura de [Wikipedia en Web Archive](https://web.archive.org/web/20230902185326/https://en.wikipedia.org/wiki/List_of_countries_by_GDP_%28nominal%29).

## Pipeline

1. **Extracción** — descarga el HTML con `requests` y parsea la tabla de países con `BeautifulSoup`.
2. **Transformación** — convierte el PIB de texto con comas a valor numérico con `pandas`/`numpy`, y lo pasa de millones a miles de millones de USD (redondeado a 2 decimales).
3. **Carga** — guarda el resultado en `Countries_by_GDP.csv` y en una base de datos SQLite (`World_Economies.db`, tabla `Countries_by_GDP`).
4. **Consulta de verificación** — ejecuta `SELECT * FROM Countries_by_GDP WHERE GDP_USD_billions >= 100` sobre la base recién cargada.
5. **Logging** — cada etapa registra un timestamp en `etl_project_log.txt` para poder medir cuánto tarda cada paso.

## Contenido

- `etl.py` — script con las funciones `extraer`, `transformar`, `cargar_a_csv`, `cargar_a_db`, `consultar` y `log_progress`.
- `Countries_by_GDP.csv` — salida del proceso.
- `Pipfile` — dependencias del entorno.

## Tecnologías

Python · pandas · NumPy · BeautifulSoup · requests · SQLite

## Cómo ejecutar

```bash
pip install pandas numpy beautifulsoup4 requests
python etl.py
```

## Autor

Horacio Laphitz — [GitHub](https://github.com/HoracioLaphitz) · [LinkedIn](https://www.linkedin.com/in/horacio-laphitz)
