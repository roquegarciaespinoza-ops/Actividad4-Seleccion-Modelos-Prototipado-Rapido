# Notebooks de la Actividad 4

Los tres cuadernos se publicaron directamente desde sus versiones disponibles en Google Drive/Colab:

| Archivo | Contenido | Celdas |
|---|---|---:|
| `Actividad4_Auditoria_Datasets_OCR.ipynb` | Auditoría inicial de datos | 12 |
| `Actividad4_Auditoria_Datasets_OCR_actualizado.ipynb` | Auditoría corregida y revisión de recortes | 20 |
| `Actividad4_Comparacion_Modelos_OCR.ipynb` | Pruebas con tres modelos de reconocimiento óptico de caracteres (OCR, *Optical Character Recognition*) | 22 |

## Publicación responsable

Se retiraron las salidas visuales incrustadas, ya que pueden contener imágenes de matrículas cuya redistribución no se ha verificado. Se conservaron las celdas de código y Markdown, así como resultados textuales en los notebooks actualizados y de comparación; en el cuaderno inicial se retiraron todas las salidas. Las versiones originales siguen en Google Colab.

## Reproducción

1. Abrir en Google Colab.
2. Usar unidad de procesamiento gráfico (GPU, *Graphics Processing Unit*) Tesla T4 o equivalente para el notebook de comparación; la auditoría puede correr en CPU.
3. Ejecutar celdas de configuración e instalación; algunas versiones de dependencias del entorno pueden variar.
4. Recuperar los conjuntos de datos de sus repositorios originales y generar los recortes.
5. Revisar la documentación sobre etiquetas automáticas no verificadas antes de interpretar métricas.

**Nota:** no hay un conjunto de evaluación completamente verificado ni se ha demostrado el objetivo de lectura correcta del 97 % del caso de negocio.
