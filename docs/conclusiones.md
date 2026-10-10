# Conclusiones y deuda técnica

## Aprendizaje obtenido
La elección de un modelo preentrenado no se resuelve únicamente comparando puntuaciones. Durante el prototipado fue necesario identificar problemas de anotación, corregir una extracción de JSON (*JavaScript Object Notation*), comprobar permisos de acceso a repositorios y reemplazar modelos que no pudieron ejecutarse de forma segura o disponible.

La auditoría previa evitó interpretar equivocadamente 150 etiquetas como vacías y reveló que un recorte geométricamente válido puede contener una etiqueta incorrecta.

## Resultados técnicos
Se ejecutaron tres modelos de reconocimiento óptico de caracteres (OCR, *Optical Character Recognition*) en Google Colab con una unidad de procesamiento gráfico (GPU, *Graphics Processing Unit*) Tesla T4. Los tres produjeron inferencias sobre las mismas 12 imágenes y se calcularon exactitud, precisión por caracteres, exhaustividad, puntuación F1, tasa de error por carácter y latencia.

TrOCR Base Printed mostró la mayor coincidencia con las etiquetas automáticas, aunque con mayor latencia. TrOCR Small Printed fue más rápido y TrOCR Small Handwritten mostró el costo de utilizar un modelo entrenado para un dominio distinto.

## Evaluación posterior sobre referencias revisadas

Se revisaron doce recortes; se aceptaron diez y se excluyeron dos por ilegibilidad. Sobre las diez matrículas aceptadas, TrOCR Base Printed obtuvo **7/10 coincidencias exactas (70 %)** y **85.33 % de F1 por caracteres**, mientras que TrOCR Small Printed obtuvo 6/10 (60 %) y 75.87 % de F1. Se mantiene TrOCR Base como modelo recomendado **para continuar prototipado**, sin validación productiva.

## Alcance de la conclusión
**Las métricas son exclusivamente exploratorias.** La verificación humana de etiquetas no se completó y el conjunto tiene ejemplos inadecuados para la tarea. No se demuestra precisión del 97 %, ausencia de falsas autorizaciones ni viabilidad productiva del control de acceso.

## Ajustes mínimos realizados
Se estandarizaron las entradas mediante recortes y normalización de caracteres, se seleccionó GPU y se mantuvo una misma muestra para los tres modelos. **No se hizo ajuste fino (*fine-tuning*) ni entrenamiento de pesos**, pues la etapa buscaba validar modelos preentrenados con bajo costo inicial.

## Deuda técnica priorizada
1. Completar una muestra de evaluación de matrículas con transcripciones humanas verificadas.
2. Asegurar diversidad geográfica y operacional, especialmente formatos mexicanos, iluminación y placas de dos líneas.
3. Comprobar ausencia de solapamiento con datos de entrenamiento y errores sistemáticos.
4. Verificar licencias de uso, permisos de publicación, privacidad y retención de imágenes.
5. Repetir mediciones de latencia y memoria con cargas realistas y registrar versiones exactas.
6. Evaluar el componente previo de detección de matrículas y el posterior de validación de autorizaciones, sin apertura física automática en esta fase.

## Próxima decisión
Conservar a TrOCR Base Printed como **candidato preliminar** y revaluarlo junto a otras alternativas especializadas cuando existan referencias verificadas. La decisión de producción se aplaza hasta contar con evidencia suficiente y controles de seguridad.
