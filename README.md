# INEGIpy_v2

Librería de Python para consultar indicadores económicos y sociales del INEGI a través de su API oficial.

Esta librería permite:
- Consultar indicadores del INEGI (Banco de Indicadores y el Banco de Información Económica)
- Recuperar metadatos asociados a los indicadores

---

## 🧭 Origen del proyecto

**INEGIpy_v2 está basada en la librería original [`INEGIpy`](https://pypi.org/project/INEGIpy/)**.

Esta versión surge como una **revisión** de la librería original, con los siguientes objetivos:

Todo el crédito por la idea original que corresponde a los autores de **INEGIpy**.

---

## 📦 Instalación

### Desde GitHub (recomendado por ahora)

```bash
pip install git+https://github.com/claudiodanielpc/INEGIpy_v2.git
```

🔑 Requisitos

Token de acceso al API del INEGI
(puede obtenerse en: https://www.inegi.org.mx/servicios/api_indicadores.html)

🚀 Ejemplos de uso
📌 1. Consultar un solo indicador

Ejemplo para obtener la población total de México entre 2000 y 2010.

```bash
from INEGIpy_v2.indicadores import Indicadores

api = Indicadores(token="TU_TOKEN_INEGI")

df = api.obtener_df(
    indicadores="100200001",
    nombres="Población total",
    inicio="2000",
    fin="2010"
)

df
```
Resultado:

Regresa un DataFrame con índice de fechas

Una columna con el nombre definido por el usuario

| fechas      | Población total |
|------------|-----------------|
| 2000-01-01 | 97,483,412.0    |
| 2005-01-01 | 103,263,388.0   |
| 2010-01-01 | 112,336,538.0   |



📌 2. Consultar múltiples indicadores

Ejemplo para obtener población total, hombres y mujeres en el mismo periodo.
```bash
varios = api.obtener_df(
    indicadores=["100200001", "100200002", "100200003"],
    nombres=["Población total", "Hombres", "Mujeres"],
    inicio="2000",
    fin="2010"
)

varios
```

Resultado:

Un DataFrame con una columna por indicador

Todas las series alineadas por fecha

| fechas      | Población total | Hombres     | Mujeres     |
|------------|-----------------|-------------|-------------|
| 2000-01-01 | 97,483,412.0    | 47,592,253.0 | 49,891,159.0 |
| 2005-01-01 | 103,263,388.0   | 50,249,955.0 | 53,013,433.0 |
| 2010-01-01 | 112,336,538.0   | 54,855,231.0 | 57,481,307.0 |


📌 Consultar indicadores con metadatos

Si además de la serie de tiempo se requiere obtener los metadatos del indicador, se puede usar el parámetro metadatos=True.

🧩 Código de ejemplo
```bash
from INEGIpy_v2.indicadores import Indicadores

api = Indicadores(token="TU_TOKEN_INEGI")

df, metadatos = api.obtener_df(
    indicadores="100200001",
    nombres="Población total",
    inicio="2000",
    fin="2010",
    metadatos=True
)

display(df)
display(metadatos)
```

| fechas      | Población total |
|------------|-----------------|
| 2000-01-01 | 97,483,412.0    |
| 2005-01-01 | 103,263,388.0   |
| 2010-01-01 | 112,336,538.0   |


| Clave       | Población total |
|------------|-----------------|
| INDICADOR  | 100200001       |
| FREQ       | 7               |
| TOPIC      | 123             |
| UNIT       | 188             |
| UNIT_MULT  | —               |
| NOTE       | 1398            |
| SOURCE     | 2,3,343,487,781,1668,1669,1670,1671,1672,1677,… |
| LASTUPDATE | 21/10/2024 12:00 a. m. |
| STATUS     | None            |
| BANCO      | BISE            |

