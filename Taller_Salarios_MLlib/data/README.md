# Datos: Census Income (Adult)

Los datos no se incluyen en el repositorio. Se descargan de la fuente original:

1. Entrar a https://archive.ics.uci.edu/dataset/20/census+income y descargar el zip.
2. Descomprimirlo y tomar `adult.data` (32 561 registros) y `adult.test` (16 281 registros).
3. Subir los dos archivos a la misma carpeta de Jupyter donde está `BuenoSalario_1055.ipynb`. Las primeras celdas del cuaderno los copian a HDFS (`/Formatos1055/BuenoLuis/Salario`).

| Archivo | Registros | Particularidades |
|---|---|---|
| `adult.data` | 32 561 | Sin encabezado, valores separados por `, `, faltantes como `?` |
| `adult.test` | 16 281 | Igual que el anterior, más una primera línea `\|1x3 Cross validator` y etiquetas terminadas en punto (`>50K.`) |

**Licencia:** CC BY 4.0.
**Cita:** Kohavi, R. (1996). *Census Income* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5GP7S
