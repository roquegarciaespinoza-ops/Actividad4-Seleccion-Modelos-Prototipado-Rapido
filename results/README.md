# Evidencias experimentales

Los siguientes archivos se recuperaron del paquete `Actividad4_Resultados_GitHub.zip` generado por Google Colab:

| Archivo | Función |
|---|---|
| `fichas_modelos.csv` | Candidatos de la etapa inicial, **antes** de sustituir GOT-OCR 2.0 |
| `estado_modelos_parcial.csv` | Resultado histórico: primeros dos TrOCR ejecutados |
| `estado_modelos.csv` | Estado final: tres modelos ejecutados correctamente |
| `metricas_resumen.csv` | Métricas y latencias experimentales sobre doce ejemplos por modelo |
| `predicciones_detalle.csv` | 36 predicciones con identificación de recorte, latencia y métricas individuales |
| `conclusiones_preliminares.md` | Salida histórica generada automáticamente por el notebook |

El conjunto utilizado se describe en `../data/muestra_evaluada.csv`.

**Advertencia metodológica:** las etiquetas son automáticas y figuran como `sin_verificar`. Los valores representan coincidencia exploratoria con referencias no certificadas; no deben interpretarse como precisión operativa ni cumplimiento del objetivo del 97 %.

**Control de versiones:** las fichas de selección registran GOT-OCR 2.0 porque se generaron antes del cambio; el modelo final fue **TrOCR Small Handwritten**. La nota de `conclusiones_preliminares.md` que solicita todavía ejecutar los tres modelos también es histórica: el archivo definitivo `estado_modelos.csv` confirma que se ejecutaron los tres. Se conservan esos registros sin alterar el contexto de su generación.

Los archivos CSV se transcribieron desde los resultados recuperados del ZIP para su publicación. El ZIP original permanece disponible en la conversación; la reproducibilidad debe comprobarse ejecutando los notebooks.
