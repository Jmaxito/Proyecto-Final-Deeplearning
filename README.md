# Clasificación de Malezas y Cultivo de Sorgo con Deep Learning  
Modelos CNN y ResNet18 desde cero

Este repositorio contiene el pipeline completo para entrenar, evaluar y comparar modelos de **clasificación de imágenes agrícolas**, utilizando el dataset **SorghumWeedDataset_Classification**, el cual contiene imágenes de:

- **Clase 0** – Plantas de sorgo  
- **Clase 1** – Pastos  
- **Clase 2** – Malezas

Se implementaron dos arquitecturas desde cero:

1. **CNN desarrollada en Keras**  
2. **ResNet18 desarrollada manualmente en PyTorch (sin transfer learning)**  

El objetivo es evaluar el rendimiento de arquitecturas simples vs. redes profundas sin pesos preentrenados en un dataset moderado (~4,300 imágenes).

---

## Estructura del Dataset
El dataset se compone de 4312 imagenes, Train:3019, Val:862, Test:431. Cada una contiene las clases: Calss0_Sorghum, Class1_Grass, Class2_BroadLeafWeed
El dataset debe organizarse en formato estándar de clasificación:

├── train/

│ ├── class0/

│ ├── class1/

│ └── class2/

├── val/

│ ├── class0/

│ ├── class1/

│ └── class2/

└── test/

├── class0/

├── class1/

└── class2/

Cada imagen fue redimensionada a **224 × 224 px**.

---

# Modelos Utilizados

##  1. CNN (Keras – Training from Scratch)

Arquitectura simple con:
- Convoluciones 2D
- MaxPooling
- Dropout
- Capa densa final softmax

##  2. ResNet18 (PyTorch – Training from Scratch)

Implementación manual de:
- BasicBlock (bloques residuales)
- Arquitectura original (2 bloques por etapa)
- Sin pesos preentrenados de ImageNet

---

#  Resultados

Los experimentos se realizaron en Google Colab (GPU cuando disponible).  
Los resultados reportados son los obtenidos tras el entrenamiento completo en el *set de prueba*.

##  Métricas Finales

###  CNN (Keras)
- **Accuracy entrenamiento:** 0.9038  
- **Loss entrenamiento:** 0.2962  
- **Accuracy test:** 0.8724  
- **Loss test:** 0.3907  

###  ResNet18 (PyTorch desde cero)
- **Accuracy test:** 0.8353  
- **Loss test:** 0.4348  

---

#  Tabla Comparativa

| Característica | CNN (Keras) | ResNet18 (PyTorch – desde cero) |
|----------------|-------------|----------------------------------|
| Arquitectura | CNN simple | ResNet18 completa |
| Entrenamiento | Desde cero | Desde cero |
| Preentrenamiento | ❌ No | ❌ No |
| Accuracy (test) | **0.8724** | 0.8353 |
| Loss (test) | **0.3907** | 0.4348 |
| Tamaño del modelo | Pequeño | Grande |
| Riesgo de Overfitting | Bajo | Medio |
| Velocidad de entrenamiento | Lenta | Rápida |
| Generalización | **Alta** | Buena |
| Complejidad | Baja | Alta |

---

#  Conclusiones

- La **CNN**, a pesar de ser más pequeña y simple, logró **mejor generalización** que ResNet18 desde cero.  
- La **ResNet18** demostró ser potente, pero al no utilizar transfer learning requiere más datos y regularización para alcanzar su máximo rendimiento.
- Esto confirma que en datasets agrícolas de tamaño medio, **las arquitecturas pequeñas desde cero pueden superar a redes profundas no preentrenadas**.

Se recomienda probar este proyecto con:
- Transfer Learning en ResNet18 y MobileNetV2  
- Data augmentation avanzado  
- Mezcla de técnicas como CutMix o MixUp  

---

#  Cómo Reproducir el Proyecto

### 1. Clonar el repositorio:

```bash
git clone https://github.com/usuario/tu-repo.git
cd tu-repo
