# Datos: Census Income (Adult)

Esta carpeta trae los dos archivos que usa el cuaderno:

| Archivo | Registros | Particularidades |
|---|---|---|
| `adult.data` | 32 561 | Sin encabezado, valores separados por `, `, faltantes como `?` |
| `adult.test` | 16 281 | Igual que el anterior, más una primera línea `\|1x3 Cross validator` y etiquetas terminadas en punto (`>50K.`) |

**Para correr el cuaderno en el clúster**, sube estos dos archivos a la misma carpeta de Jupyter donde está `BuenoSalario_1055.ipynb`. Las primeras celdas los copian a HDFS (`/Formatos1055/BuenoLuis/Salario`).

**Procedencia.** `adult.data` coincide línea por línea con el archivo original. `adult.test` tiene los mismos 16 281 registros y el mismo formato del original, y se reconstruyó a partir de una copia completa del dataset. Si se quiere la copia exacta de UCI, se puede reemplazar por la del zip oficial: el cuaderno funciona igual con cualquiera de las dos.

**Fuente original:** https://archive.ics.uci.edu/dataset/20/census+income
**Licencia:** CC BY 4.0. Se redistribuye aquí con la cita correspondiente.
**Cita:** Kohavi, R. (1996). *Census Income* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5GP7S
