# Caso de uso — control de acceso vehicular

## Contexto y problema
Este trabajo da continuidad a **Fase I - Business Case - Unidad Habitacional TecMilenio**. El problema empresarial consiste en controlar el ingreso de vehículos, de forma que solamente los vehículos autorizados puedan acceder. El caso de negocio contempla un sistema de reconocimiento de matrículas vinculado a un padrón de autorizaciones.

## Alcance de la Actividad 4
El prototipo académico evalúa exclusivamente el reconocimiento óptico de caracteres (OCR, *Optical Character Recognition*) sobre **imágenes en las que la región de la matrícula ya está recortada**. No realiza detección automática de matrículas en escenas completas, consulta a residentes, autorización del acceso ni accionamiento de barreras.

### Entrada y salida
- **Entrada:** recorte de una región potencialmente correspondiente a una matrícula vehicular.
- **Salida:** secuencia de caracteres reconocidos, acompañada de tiempo de inferencia.
- **Unidad de evaluación:** matrícula completa normalizada; también se comparan caracteres mediante alineación.

## Criterios de éxito
La evaluación académica solicita exactitud (*accuracy*), precisión (*precision*), exhaustividad (*recall*), puntuación F1 (*F1-score*) y latencia. Se añadió la tasa de error por carácter (CER, *Character Error Rate*) por su relevancia para OCR.

El objetivo de lectura correcta del **97 %** proviene del caso de negocio y es una **meta**, no un resultado alcanzado. Los datos disponibles son exploratorios y no bastan para verificarla.

## Riesgos
Etiquetas automáticas incorrectas, baja resolución, placas extranjeras o de dos líneas, iluminación y ángulos variables, diferencias entre el conjunto de prueba y matrículas mexicanas, además de riesgos de privacidad y autorizaciones.

## Decisión
Construir un prototipo rápido de reconocimiento antes de invertir en la integración completa. El alcance acotado permite comparar modelos en una misma unidad de procesamiento gráfico (GPU, *Graphics Processing Unit*) de Google Colab y registrar deuda técnica sin afirmar que la solución está lista para producción.
