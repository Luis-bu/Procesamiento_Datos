# Procesamiento de Datos a Gran Escala

**Autor:** Luis Bueno
**Universidad:** Pontificia Universidad Javeriana — Bogotá
**Programa:** Ingeniería de Sistemas — VI Semestre
**Curso:** Procesamiento de Datos a Gran Escala (código de clase 1055) — Prof. John Jairo Corredor Franco, PhD
**Contacto:** bu_luis@javeriana.edu.co
**GitHub:** [github.com/Luis-bu](https://github.com/Luis-bu)

Repositorio con los laboratorios y talleres del curso. Cada carpeta es una entrega independiente, con sus cuadernos y su propio README.

## Contenido

| Carpeta | Entrega | Tecnologías |
|---------|---------|-------------|
| [`Lab01_Python/`](Lab01_Python/) | Lab 01: fundamentos de Python (cadenas, tuplas, listas, conjuntos, diccionarios, condiciones, bucles, funciones, clases) + cuaderno bono | Python, Jupyter |
| [`Taller_Salarios_MLlib/`](Taller_Salarios_MLlib/) | Taller de modelos de clasificación: predicción de salarios (Census Income, UCI) con 7 modelos de MLlib, validación cruzada y modelo guardado en HDFS | PySpark, Spark MLlib, Hadoop HDFS |

## Estructura

```
Procesamiento_Datos/
├── README.md
├── .gitignore
├── Lab01_Python/
│   ├── README.md
│   ├── 01-Python-Cadenas.ipynb ... 09-Python-Clases.ipynb
│   └── Practico_Bono_1.ipynb
└── Taller_Salarios_MLlib/
    ├── README.md
    ├── BuenoSalario_1055.ipynb
    ├── requirements.txt
    └── data/
        └── README.md
```

## Entorno

Los cuadernos de Python corren en cualquier instalación de Jupyter. Los talleres de Spark se desarrollaron en el clúster del curso (Jupyter + Apache Spark 3.5 + Hadoop HDFS); cada carpeta explica cómo ejecutarlos.
