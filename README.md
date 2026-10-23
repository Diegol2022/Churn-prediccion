# Predicción de Churn — Modelado y Evaluación de Clasificación

## Descripción del problema

Una empresa de telecomunicaciones quiere anticipar qué clientes van a **abandonar el servicio (Churn)** para poder aplicar acciones de retención antes de perderlos.

En este proyecto se entrena un modelo de **clasificación binaria (Logistic Regression)** sobre el dataset *Telco Customer Churn* de IBM. El dataset tiene 7.043 clientes y 21 variables: datos demográficos, servicios contratados, tipo de contrato y facturación. El desempeño se evalúa con **Accuracy, Precision, Recall, F1-Score y Matriz de Confusión**.

## Estructura del repositorio

```
.
├── data/
│   └── Telco-Customer-Churn.csv   # Dataset
├── modelado_metricas.ipynb        # Notebook: carga, split 80/20, modelo, métricas y conclusión
├── requirements.txt               # Dependencias
├── .gitignore
└── README.md
```

## Datos: de dónde descargarlos

El dataset **ya viene incluido** en el repositorio, en `data/Telco-Customer-Churn.csv`. Si por algún motivo no está, o querés bajarlo de nuevo, podés descargarlo desde cualquiera de estas fuentes.

**Opción A: repositorio oficial de IBM en GitHub (recomendada)**
1. Entrá a la página del archivo: [github.com/IBM/telco-customer-churn-on-icp4d/blob/master/data/Telco-Customer-Churn.csv](https://github.com/IBM/telco-customer-churn-on-icp4d/blob/master/data/Telco-Customer-Churn.csv).
2. Hacé clic en el botón de descarga (**Download raw file**, el ícono ⬇ arriba a la derecha del archivo).
3. El archivo ya se llama `Telco-Customer-Churn.csv`, no hace falta renombrarlo.

**Opción B: Kaggle**
1. Entrá a [kaggle.com/datasets/blastchar/telco-customer-churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn). Necesitás una cuenta gratuita de Kaggle.
2. Hacé clic en **Download** y descomprimí el `.zip`.
3. El archivo se llama `WA_Fn-UseC_-Telco-Customer-Churn.csv`. **Renombralo** a `Telco-Customer-Churn.csv`.

**Dónde guardarlo:** en ambos casos, poné el archivo dentro de la carpeta `data/` del proyecto, junto al notebook:

```
<carpeta-del-proyecto>/
├── data/
│   └── Telco-Customer-Churn.csv   ← acá
└── modelado_metricas.ipynb
```

Si la carpeta `data/` no existe, creala. El notebook busca el archivo exactamente en la ruta `data/Telco-Customer-Churn.csv`.

---

## Paso a paso para ejecutar el notebook en Visual Studio Code

### Paso 1: Instalar los programas necesarios

Esto se hace una sola vez por computadora.

1. **Python 3.9 o superior:** descargalo desde [python.org/downloads](https://www.python.org/downloads/).
   - **En Windows**, durante la instalación tildá la casilla **"Add python.exe to PATH"**. Es importante.
   - Para verificar que quedó instalado, abrí una terminal y escribí:
     ```bash
     python --version
     ```
     En Mac o Linux puede ser `python3 --version`.
2. **Visual Studio Code:** descargalo desde [code.visualstudio.com](https://code.visualstudio.com/).
3. **Git:** descargalo desde [git-scm.com](https://git-scm.com/downloads). Solo lo necesitás si vas a clonar el repositorio.

### Paso 2: Descargar el proyecto

**Opción A: con Git.** Abrí una terminal y ejecutá:
```bash
git clone https://github.com/<tu-usuario>/<nombre-del-repo>.git
```

**Opción B: sin Git.** En la página del repositorio en GitHub, hacé clic en **Code → Download ZIP** y descomprimilo.

Después verificá que exista el archivo `data/Telco-Customer-Churn.csv`. Si no está, descargalo como se explica en la sección [Datos: de dónde descargarlos](#datos-de-dónde-descargarlos).

### Paso 3: Abrir la carpeta en VS Code

1. Abrí VS Code.
2. Andá a **File → Open Folder…** (en español, **Archivo → Abrir carpeta…**).
3. Elegí la carpeta del proyecto, la que contiene `modelado_metricas.ipynb` y la carpeta `data/`.
   - Abrí la carpeta, no el notebook suelto. Así el notebook encuentra el dataset en `data/`.
4. Si VS Code pregunta *"Do you trust the authors of the files in this folder?"*, respondé **Yes, I trust the authors**.

### Paso 4: Instalar las extensiones de Python y Jupyter

1. Abrí la pestaña de **Extensiones** con `Ctrl+Shift+X` (en Mac, `Cmd+Shift+X`).
2. Buscá e instalá estas dos extensiones de Microsoft:
   - **Python**
   - **Jupyter**

### Paso 5: Crear el entorno virtual e instalar las dependencias

El entorno virtual (`.venv`) mantiene las librerías del proyecto aisladas del resto de tu computadora.

**Forma 1: desde el menú de VS Code (recomendada)**
1. Presioná `Ctrl+Shift+P` (en Mac, `Cmd+Shift+P`).
2. Escribí **Python: Create Environment** y presioná Enter.
3. Elegí **Venv**.
4. Elegí tu versión de Python (3.9 o superior).
5. Cuando pregunte por dependencias, tildá **requirements.txt** y aceptá.
6. Esperá a que termine. Abajo a la derecha vas a ver el progreso.

**Forma 2: desde la terminal de VS Code**

Abrí la terminal con **Terminal → New Terminal** (o `` Ctrl+` ``) y ejecutá:

En **Windows**:
```powershell
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

En **Mac o Linux**:
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Si quedó bien activado, vas a ver `(.venv)` al principio de la línea de la terminal.

### Paso 6: Abrir el notebook y elegir el kernel

1. En el explorador de archivos de VS Code (a la izquierda), hacé clic en `modelado_metricas.ipynb`.
2. Arriba a la derecha del notebook, hacé clic en **Select Kernel**.
3. Elegí **Python Environments…** y después **.venv**.
4. Si VS Code pide instalar `ipykernel`, aceptá con **Install**.

### Paso 7: Ejecutar el notebook

- Hacé clic en **Run All** (▶▶) en la barra superior del notebook para correr todas las celdas en orden.
- También podés ejecutar las celdas de a una: hacé clic en el ▶ a la izquierda de cada celda, o presioná `Shift+Enter`.
- Para empezar de cero, usá **Restart** y después **Run All**.

**Qué vas a ver:**
- la carga y exploración de los datos;
- la división Train/Test 80/20 y el entrenamiento de la Logistic Regression;
- las métricas Accuracy, Precision, Recall y F1-Score;
- la matriz de confusión como mapa de calor;
- la interpretación de las métricas y la conclusión de negocio.

---

## Problemas frecuentes

| Problema | Solución |
|---|---|
| `'python' no se reconoce como un comando` (Windows) | Python no se agregó al PATH. Reinstalalo tildando **"Add python.exe to PATH"**, o probá con `py` en lugar de `python`. |
| En PowerShell: *"la ejecución de scripts está deshabilitada en este sistema"* al activar `.venv` | Ejecutá `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned`, respondé `S`, y volvé a activar. También podés cambiar la terminal a **Command Prompt** desde el menú ⌄ de la terminal. |
| `ModuleNotFoundError: No module named 'pandas'` (u otra librería) | El kernel no es `.venv` (ver el Paso 6), o faltó instalar las dependencias: ejecutá `pip install -r requirements.txt` con el entorno activado. |
| `FileNotFoundError: data/Telco-Customer-Churn.csv` | Abriste el notebook suelto y no la carpeta del proyecto (ver el Paso 3), o falta el CSV dentro de `data/`. En ese caso, descargalo como se explica en la sección **Datos: de dónde descargarlos** y verificá que tenga exactamente ese nombre. |
| No aparece `.venv` en **Select Kernel** | Cerrá y volvé a abrir VS Code, o elegí **Python Environments…** y esperá a que cargue la lista. |
| El notebook pide `ipykernel` | Aceptá **Install**, o ejecutá `pip install ipykernel` con el entorno activado. |

### Alternativa: Jupyter desde la terminal

Si preferís no usar VS Code, con el entorno activado podés ejecutar:
```bash
jupyter notebook modelado_metricas.ipynb
```
Se abre en el navegador. Ahí usá **Kernel → Restart & Run All**.

---

## Resumen de resultados

El set de prueba tiene 1.407 clientes (el 20% del total, estratificado). De ellos, 374 abandonaron.

| Métrica | LogReg base | LogReg balanceada (`class_weight="balanced"`) |
|---|---|---|
| Accuracy | 0,805 | 0,726 |
| Precision | 0,650 | 0,490 |
| **Recall** | **0,575** | **0,797** |
| F1-Score | 0,610 | 0,607 |
| Falsos Negativos | 159 | 76 |
| Falsos Positivos | 116 | 310 |

**Matriz de confusión (modelo base):** VN = 917 · FP = 116 · FN = 159 · VP = 215

### Conclusión

- La métrica más importante para Churn es el **Recall**. Un **falso negativo** es un cliente que se va sin que el modelo lo detecte: se pierden sus ingresos futuros sin chance de intervenir. En cambio, un falso positivo solo cuesta una acción de retención innecesaria.
- El modelo base tiene buen Accuracy (80,5%), pero deja pasar 159 de los 374 clientes que se van (42,5%).
- La versión balanceada eleva el Recall a cerca del 80% y **reduce los falsos negativos a la mitad (de 159 a 76)**, a cambio de más falsos positivos. Retener un cliente suele ser más barato que perderlo y captar uno nuevo, así que esta es la opción recomendada para el negocio.

## Tecnologías

Python · pandas · NumPy · scikit-learn · matplotlib · seaborn · Jupyter · Visual Studio Code

## Fuente de datos

- [Telco Customer Churn — IBM (GitHub)](https://github.com/IBM/telco-customer-churn-on-icp4d)
- [Telco Customer Churn — Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
