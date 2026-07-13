## segmentacion-histopatologica-cancer-mama-unet-resnet34
# Segmentación semántica de tejido histopatológico de cáncer de mama mediante U-Net con backbone ResNet34

## Descripción
Este proyecto implementa un modelo de segmentación semántica basado en la arquitectura **U-Net** con un backbone **ResNet34**, entrenado para identificar y delimitar regiones de tejido canceroso en imágenes histopatológicas de cáncer de mama.

## Objetivo
Desarrollar un modelo de segmentación semántica basado en la arquitectura U-Net con backbone ResNet34 para la identificación automática de tejidos histopatológicos en imágenes de cáncer de mama, utilizando el dataset Breast Cancer Semantic Segmentation (BCSS). El proyecto busca contribuir al fortalecimiento de herramientas de apoyo diagnóstico mediante técnicas de aprendizaje profundo, optimizando métricas de segmentación como mIoU y Dice Score, y evaluando la capacidad de generalización del modelo sobre diferentes clases tisulares clínicamente relevantes.

## Tecnologías utilizadas
- Python, TensorFlow, librería `segmentation_models`
- Arquitectura U-Net con encoder ResNet34 preentrenado (ImageNet), con fine-tuning completo
- Función de pérdida: Dice Loss + Categorical Focal Loss (con pesos por clase para mitigar el desbalance)
- Optimizador Adam (learning rate inicial 1×10⁻⁴), Early Stopping y ReduceLROnPlateau
- Entrenamiento: 50 épocas, batch size 4, imágenes de 512×512 px

## Dataset
[Breast Cancer Semantic Segmentation (BCSS)](https://www.kaggle.com/datasets) — versión BCSS_512, compuesta por parches de imágenes histopatológicas de 512×512 píxeles con máscaras de segmentación. Las 22 categorías tisulares originales fueron agrupadas en 6 clases clínicamente relevantes: **Fondo, Tumor, Estroma, Linfocitos, Necrosis y Otros**.

Tras el preprocesamiento (emparejamiento imagen-máscara y eliminación de máscaras vacías) se obtuvo un total de **7,691 pares válidos**, divididos en:
- Entrenamiento: 5,383 (70%)
- Validación: 1,154 (15%)
- Prueba: 1,154 (15%)

## Resultados

**Métricas globales (conjunto de test):**
| Métrica | Valor |
|---|---|
| mIoU | 0.5822 |
| Dice Score | 0.6714 |
| AUC-ROC | 0.9300 |

**IoU por clase (test):**
| Clase | IoU |
|---|---|
| Tumor | 0.8421 |
| Estroma | 0.8113 |
| Necrosis | 0.6928 |
| Linfocitos | 0.6310 |

El modelo mostró el mejor desempeño en las clases **Tumor** y **Estroma**, evidenciando una adecuada capacidad de discriminación tisular. El uso de *class weights* y el descongelamiento del encoder contribuyeron a mejorar la generalización, especialmente en clases minoritarias como Linfocitos y Necrosis. La clase **Otros** fue la más difícil de generalizar, dado que agrupa estructuras heterogéneas.

## Contenido del repositorio
- `PIF_TIA_cancer_VFinal.ipynb` — Notebook con el desarrollo completo del proyecto
- `docs/` — Presentación del proyecto

## 👤 Autora
Carolina Novoa
