# Auditoría de los conjuntos de datos

## Propósito
Antes de evaluar los modelos se revisaron las fuentes de datos para comprobar la estructura de las etiquetas, la posibilidad de extraer matrículas y las limitaciones que afectan la validez de las métricas. La auditoría fue **exploratoria**, no una certificación del dataset completo.

## Fuentes consideradas
- [Sonne Technology — License Plate Text Recognition Full](https://huggingface.co/datasets/sonnetechnology/license-plate-text-recognition-full), con imágenes, coordenadas de regiones y etiquetas automáticas.
- [Number Plate Recognition](https://huggingface.co/datasets/prithivMLmods/Number-Plate-Recognition), cuyas etiquetas se encontraron anidadas en el campo `response`.

## Pruebas realizadas
1. Se cargaron **150 registros por fuente** mediante *streaming*: 300 observaciones iniciales.
2. La primera versión del análisis marcó **150 etiquetas vacías** para Number Plate Recognition. La inspección reveló un error del **procesamiento propio**: las matrículas estaban en un objeto JSON (*JavaScript Object Notation*), bajo `license_plate_number`. Tras corregirlo, se recuperaron las 150 transcripciones. Esta corrección es evidencia del valor de revisar los esquemas antes de descartar un dataset.
3. En Sonne se generaron **160 recortes de 150 imágenes**. Todas las coordenadas resultaron **geométricamente válidas**; ello no garantiza que las etiquetas correspondan a placas reales o legibles.
4. La inspección visual de recortes identificó etiquetas parciales o incorrectas, regiones ajenas a matrículas y placas de una o dos líneas.
5. La priorización por reglas exploratorias arrojó **30 recortes de prioridad alta, 75 media y 55 baja**. Las alertas incluyeron resolución reducida (70), etiqueta muy corta (38), ausencia de letras (37), ausencia de números (36), caracteres no habituales (22) y contraste bajo (2). Varias alertas pueden recaer en un mismo recorte; **no son tasas de error confirmadas**.

## Decisión y limitaciones
Se eligió Sonne como fuente operativa para el experimento porque dispone de coordenadas de recorte. Sin embargo, **no se concluyó la verificación humana**. La interfaz de revisión manual se probó, pero no se confirmó una tabla completa de transcripciones revisadas y guardadas. Por tanto, las etiquetas automáticas se conservaron únicamente para una **evaluación exploratoria**.

No se deben inferir porcentajes de calidad para la totalidad del dataset a partir de los registros iniciales, ni presentar las etiquetas como datos de referencia certificados.

## Deuda técnica
- Verificar manualmente las transcripciones que se utilizarán para evaluación formal.
- Corregir o eliminar regiones que no contienen matrículas.
- Comprobar duplicados semánticos y posible contaminación con entrenamiento.
- Incorporar matrículas mexicanas y condiciones operativas variadas.
- Conservar un registro reproducible de aceptación, corrección y descarte.
- Comprobar licencias de uso y redistribución de imágenes antes de publicarlas.

## Salidas esperadas
El notebook de auditoría y los archivos de resultados originales se incorporarán por separado tras verificar su versión final. Esta narración recoge los **resultados observados en Colab**, no sustituye esas evidencias ejecutables.
