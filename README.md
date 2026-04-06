# Checkpoint 6 — Aprendizaje de Máquina
## Clasificación de Automóviles con Árbol de Decisión y Bosque Aleatorio

---

## Descripción del ejercicio

Este ejercicio corresponde al **Checkpoint 6** de la materia de Aprendizaje de Máquina. El objetivo es aplicar y comparar dos algoritmos de clasificación supervisada — **Árbol de Decisión** y **Bosque Aleatorio** — sobre el dataset de evaluación de automóviles, con el fin de predecir la categoría de aceptabilidad de un vehículo en función de sus características.

---

## Dataset

El archivo `automoviles.csv` contiene **1727 registros** con las siguientes columnas:

| Columna | Tipo | Valores posibles | Descripción |
|---|---|---|---|
| `buying` | Categórica ordinal | `low`, `med`, `high`, `vhigh` | Precio de compra |
| `maint` | Categórica ordinal | `low`, `med`, `high`, `vhigh` | Costo de mantenimiento |
| `doors` | Categórica ordinal | `2`, `3`, `4`, `5more` | Número de puertas |
| `persons` | Categórica ordinal | `2`, `4`, `more` | Capacidad de personas |
| `lug_boot` | Categórica ordinal | `small`, `med`, `big` | Tamaño del maletero |
| `safety` | Categórica ordinal | `low`, `med`, `high` | Nivel de seguridad |
| `class` | Categórica (target) | `unacc`, `acc`, `good`, `vgood` | **Evaluación del automóvil** |

La variable objetivo `class` presenta un desbalance natural: la mayoría de registros corresponde a la categoría `unacc` (inaceptable), lo que es un aspecto relevante a considerar en la evaluación de los modelos.

---

## Estructura del proyecto

```
checkpoint-6/
│
├── automoviles.csv                  # Dataset original
├── automoviles_clasificacion.ipynb  # Notebook principal
├── requirements.txt                 # Dependencias del proyecto
└── README.md                        # Este archivo
```

---

## Flujo del notebook

### 1. Exploración de datos
Se analiza la forma del dataset, los tipos de datos, la ausencia de valores nulos y la distribución de cada variable, incluyendo una gráfica de la variable objetivo.

### 2. Preprocesamiento
Dado que todas las variables independientes son **categóricas ordinales**, se aplica un mapeo numérico que respeta el orden natural de cada atributo (por ejemplo, `low=0 < med=1 < high=2 < vhigh=3`). La variable objetivo se codifica con `LabelEncoder`. El dataset se divide en **80% entrenamiento y 20% prueba**, con estratificación para mantener la proporción de clases.

### 3. Modelo 1 — Árbol de Decisión (`DecisionTreeClassifier`)
- Entrenamiento con profundidad máxima de 6 niveles.
- Evaluación con exactitud, reporte de clasificación y matriz de confusión.
- Visualización gráfica del árbol (primeros 3 niveles).
- Validación cruzada de 5 pliegues.

### 4. Modelo 2 — Bosque Aleatorio (`RandomForestClassifier`)
- Ensamble de 100 árboles entrenados en paralelo.
- Misma evaluación que el modelo anterior.
- Gráfica de importancia de características (índice Gini).
- Validación cruzada de 5 pliegues.

### 5. Comparación de modelos
Tabla y gráfica comparativa de exactitud en el conjunto de prueba y en validación cruzada, con análisis de los trade-offs entre ambos modelos.

---

## Algoritmos utilizados

### Árbol de Decisión
Modelo que aprende reglas de decisión jerárquicas a partir de los datos. Divide el espacio de características de forma recursiva eligiendo en cada nodo la variable y el umbral que mejor separan las clases (criterio Gini). Su principal ventaja es la **interpretabilidad**: el árbol puede visualizarse y sus reglas pueden leerse de forma directa. Como desventaja, tiende al sobreajuste cuando no se limita su profundidad.

### Bosque Aleatorio
Método de ensamble que construye múltiples árboles de decisión entrenados con subconjuntos aleatorios de los datos y las características (*bagging*). La predicción final es la **votación mayoritaria** entre todos los árboles. Al promediar muchos modelos con varianza individual, el bosque aleatorio reduce el sobreajuste y generalmente obtiene una exactitud superior al árbol individual, a costa de menor interpretabilidad.

---

## Instalación y ejecución

**1. Clonar o descargar el repositorio y entrar a la carpeta:**
```bash
cd checkpoint-6
```

**2. Instalar las dependencias:**
```bash
pip install -r requirements.txt
```

**3. Abrir el notebook:**
```bash
jupyter lab automoviles_clasificacion.ipynb
```

**4. Ejecutar todas las celdas** con `Run > Run All Cells` o `Shift + Enter` celda por celda.

> **Nota:** asegúrate de que el archivo `automoviles.csv` esté en la misma carpeta que el notebook antes de ejecutarlo.

---

## Dependencias

| Librería | Uso |
|---|---|
| `pandas` | Carga y manipulación del dataset |
| `numpy` | Operaciones numéricas |
| `scikit-learn` | Modelos, métricas y preprocesamiento |
| `matplotlib` | Visualizaciones |
| `seaborn` | Estilos y gráficas estadísticas |
| `category_encoders` | Codificación de variables categóricas ordinales |
| `jupyterlab` | Entorno de ejecución del notebook |

---

## Materia
Aprendizaje de Máquina — **Checkpoint 6**
