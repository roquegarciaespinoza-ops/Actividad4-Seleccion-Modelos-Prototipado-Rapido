# Actividad 4. Selección de modelos y prototipado rápido

**Proyecto de continuidad:** Fase I - Business Case - Unidad Habitacional TecMilenio  
**Caso de uso:** reconocimiento automatizado de matrículas como componente de un sistema inteligente de control de acceso vehicular.  
**Entorno:** Google Colab con unidad de procesamiento gráfico (GPU, *Graphics Processing Unit*).  
**Ecosistema:** Hugging Face (Models, Datasets y Spaces).

## Objetivo

Seleccionar, implementar y comparar tres modelos preentrenados de reconocimiento óptico de caracteres (OCR, *Optical Character Recognition*) sobre imágenes recortadas de matrículas vehiculares, para identificar el candidato con mejor equilibrio entre calidad de lectura, latencia y recursos requeridos.

Este prototipo **no controla barreras físicas, no valida autorizaciones contra el padrón de residentes y no constituye una solución lista para producción**.

## Antecedentes y decisiones

Se retoma el caso de negocio de control de acceso de la Unidad Habitacional TecMilenio. Para delimitar el trabajo se decidió evaluar exclusivamente el reconocimiento de texto sobre recortes de matrículas; la detección de placas en imágenes completas y la integración con torniquetes o barreras quedan fuera de alcance.

Antes de seleccionar los modelos se auditó la calidad de los datos: esta decisión responde a que una etiqueta automática incorrecta puede producir una evaluación engañosa. La documentación registra las dificultades y correcciones, sin ocultar los intentos fallidos.

## Modelos implementados

| Modelo | Identificador en Hugging Face | Propósito |
|---|---|---|
| TrOCR Small Printed | `microsoft/trocr-small-printed` | Referencia de texto impreso, relativamente ligera |
| TrOCR Base Printed | `microsoft/trocr-base-printed` | Comparación de desempeño frente a un modelo de mayor tamaño |
| TrOCR Small Handwritten | `microsoft/trocr-small-handwritten` | Contraste experimental de dominio: manuscrito frente a matrículas impresas |

**Sustituciones documentadas:** el modelo especializado `DunnBC22/trocr-base-printed_license_plates_ocr` devolvió acceso HTTP 401 desde Google Colab y no se utilizó. GOT-OCR 2.0 fue considerado, pero no se ejecutó al requerir revisión y autorización de código remoto. El tercer modelo finalmente ejecutado fue TrOCR Small Handwritten. Los tres modelos implementados pertenecen a la familia TrOCR; **no representan tres arquitecturas diferentes**.

## Dataset y auditoría

Se exploraron dos conjuntos de datos públicos: Sonne Technology y Number Plate Recognition. En una muestra inicial de 150 registros por fuente, se descubrió que las etiquetas del segundo estaban anidadas en un campo JSON (*JavaScript Object Notation*), no vacías. Al corregir la extracción se recuperaron 150 etiquetas.

En Sonne Technology se examinaron 150 imágenes, se identificaron 160 regiones y se generaron 160 recortes con coordenadas geométricamente válidas. La priorización automática arrojó 30 recortes de prioridad alta, 75 media y 55 baja. La inspección visual mostró errores de transcripción y algunos textos ajenos a matrículas. **La verificación humana completa no se terminó.**

**Fuente:** [Sonne Technology en Hugging Face](https://huggingface.co/datasets/sonnetechnology/license-plate-text-recognition-full).

Las imágenes originales no se redistribuirán en este repositorio sin comprobar antes sus permisos. La procedencia de las etiquetas y las limitaciones se exponen en la documentación técnica.

## Resultados exploratorios

Se ejecutaron **tres modelos sobre las mismas 12 imágenes** en Google Colab (36 inferencias). Las referencias utilizadas eran **etiquetas automáticas no verificadas**. Los valores de esta tabla no constituyen estimaciones fiables de desempeño operativo.

| Modelo | Exactitud por matrícula | Precisión por caracteres | Exhaustividad por caracteres | F1 por caracteres | CER | Latencia media |
|---|---:|---:|---:|---:|---:|---:|
| TrOCR Base Printed | 66.67 % | 84.96 % | 87.92 % | 85.26 % | 22.50 % | 113.7 ms |
| TrOCR Small Printed | 50.00 % | 73.33 % | 68.06 % | 69.55 % | 34.03 % | 56.2 ms |
| TrOCR Small Handwritten | 0.00 % | 1.68 % | 2.08 % | 1.86 % | 105.21 % | 44.1 ms |

La exactitud representa la coincidencia exacta de toda la matrícula normalizada. La precisión, la exhaustividad (*recall*) y la puntuación F1 se calcularon mediante alineación de caracteres. CER significa *Character Error Rate*, tasa de error por carácter; puede superar el 100 % cuando existen muchas inserciones.

**Interpretación:** TrOCR Base Printed obtuvo el mejor resultado exploratorio de calidad, con mayor latencia que TrOCR Small Printed. TrOCR Small Handwritten fue más rápido, pero su comportamiento no es adecuado para texto de matrículas impresas en la muestra. No se declara un ganador definitivo porque las etiquetas no están verificadas y la muestra es pequeña.

## Decisión para la siguiente fase

**Modelo de continuidad seleccionado: [TrOCR Base Printed](docs/decision_siguiente_fase.md)** (`microsoft/trocr-base-printed`). Fue el candidato con la mejor coincidencia exploratoria con las etiquetas automáticas y se considera apropiado para **continuar el desarrollo y la validación**, no para operar el acceso vehicular todavía. Se conserva TrOCR Small Printed como respaldo ante restricciones de tiempo, memoria o costo.

La elección deberá ratificarse con un conjunto de matrículas verificadas manualmente y pruebas representativas de la unidad habitacional. Ver la [justificación técnica y empresarial](docs/decision_siguiente_fase.md) y la [auditoría de cumplimiento de la rúbrica](docs/auditoria_rubrica.md).

## Organización del repositorio

- `notebooks/`: auditoría y comparación, en archivos de notebook de Python (`.ipynb`).
- `docs/`: caso de uso, auditoría, criterios técnicos, comparación y conclusiones en Markdown (`.md`).
- `data/`: muestra tabular y descripción de procedencia, sin publicar imágenes sujetas a permisos.
- `results/`: tablas y salidas numéricas de experimentos.
- `src/`: scripts de apoyo, cuando existan.
- `requirements.txt`: dependencias y consideraciones del entorno.
- `.gitignore`: exclusiones para archivos temporales y credenciales.

## Reproducibilidad

1. Abrir los notebooks en Google Colab y activar GPU T4 (o equivalente).
2. Instalar las dependencias indicadas y verificar sus importaciones. Los entornos de Colab pueden variar.
3. Descargar los conjuntos de datos desde sus fuentes; generar los recortes siguiendo la auditoría.
4. Ejecutar las inferencias sobre la misma muestra para los tres modelos, registrando versiones de paquetes y semilla 42.
5. Calcular métricas y latencias sin sustituir resultados ausentes ni presentar etiquetas automáticas como verdad verificada.
6. Para una evaluación formal, proporcionar un archivo de matrículas transcritas y verificadas manualmente antes del cálculo final.

## Limitaciones y deuda técnica

- Completar la verificación manual y depuración de las etiquetas de evaluación.
- Ampliar el tamaño de la muestra y comprobar representatividad del contexto mexicano, incluida la variación de iluminación y formatos de dos líneas.
- Verificar posibles coincidencias entre los datos de evaluación y los conjuntos de entrenamiento de modelos.
- Revisar explícitamente licencias de modelos y datasets, consumo de memoria y costos operativos.
- Repetir experimentos y medir variabilidad, además de latencia en condiciones realistas.
- Integrar detección de placa, validación contra padrón, seguridad y apertura de acceso en etapas posteriores.

## Estado del trabajo

**Prototipo experimental ejecutado, tres notebooks, documentación y archivos CSV publicados.** La validación formal de referencias, recursos y licencias sigue pendiente. No se afirma que se haya alcanzado el objetivo operativo de lectura correcta del 97 % definido en el caso de negocio.

## Referencias de las herramientas

- [Hugging Face](https://huggingface.co/)
- [Google Colab](https://colab.research.google.com/)
- [TrOCR Small Printed](https://huggingface.co/microsoft/trocr-small-printed)
- [TrOCR Base Printed](https://huggingface.co/microsoft/trocr-base-printed)
- [TrOCR Small Handwritten](https://huggingface.co/microsoft/trocr-small-handwritten)
