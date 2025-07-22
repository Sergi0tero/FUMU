# 📈 Simulación Multiagente para Predicción de Precios en el Mercado Financiero

Este proyecto implementa una simulación multiagente que predice precios financieros a corto plazo, utilizando dos tipos de agentes:

- 🧠 `agenteIA`: agente de inteligencia artificial (no detallado en este README)
- 📊 `traditionalAgent`: agente tradicional que utiliza técnicas clásicas de predicción como regresión lineal y Gradient Boosting

---

## 🚀 Objetivo

Predecir el valor **futuro** de cierre (`Close(t+1)`) de acciones, **utilizando únicamente la información presente y pasada** (`t`, `t-1`, etc.).  
El sistema permite comparar los valores reales con las predicciones realizadas por cada agente.

---

## 🧠 Agente Tradicional (`traditionalAgent`)

Este agente combina dos modelos multivariables:

| Modelo                       | Descripción |
|-----------------------------|-------------|
| 🔹 Regresión lineal         | Captura tendencias generales |
| 🔸 Gradient Boosting        | Detecta relaciones no lineales entre variables |

### 📥 Variables utilizadas como entrada (en `t`):

- `Open`, `High`, `Low`, `Volume`
- `RSI`, `SMA_20`, `MACD`

### 📤 Variable objetivo:

- `Close(t+1)` → valor de cierre **en la siguiente hora**

---

## ⚙️ Lógica de Predicción

La predicción sigue esta lógica de simulación:

1. En el instante **`t`**, el agente predice **`Close(t+1)`** usando solo datos conocidos.
2. En **`t+1`**, se obtiene el valor real y se compara con lo predicho.
3. Se registra y grafica el resultado.

---

## 📊 Resultados

Por cada acción (`Ticker`) procesada:

- Se genera un archivo Excel: `simulacion_<TICKER>.xlsx`  
- Se produce una gráfica comparativa:
  - 🔵 Precio real
  - 🟢 Predicción tradicional
  - 🟣 Predicción IA (si está habilitada)

---

## 🖥️ Estructura del Proyecto

```bash
📦 simulador-multiagente-prediccion/
├── 📘 README.md                 # Documentación general del proyecto
├── 📄 requirements.txt         # Dependencias necesarias para correr el entorno
├── 📓 main.ipynb               # Notebook principal de simulación
├── 📄 simulacion_<TICKER>.xlsx # Resultados exportados por cada acción (generados)
├── 📁 agentes/
│   ├── traditional_agent.py    # Clase del agente tradicional (regresión + boosting)
│   └── agente_ia.py            # Clase del agente IA (opcional si lo usas)
├── 📁 core/
│   ├── broker.py               # Sistema de pub/sub entre agentes
│   ├── whiteboard.py           # Memoria compartida entre agentes y entorno
│   └── data_fetcher.py         # Controlador de datos secuenciales por ticker
├── 📁 data/
│   └── historico_top10_indicadores_completos.xlsx  # Dataset original
└── 📁 resultados/
    └── graficas/               # Gráficas generadas por cada ticker (opcional)


                   +------------------+
                   |   DataFetcher    |  --> ExcelLogger (cada hora)
                   +------------------+
                             |
                         [Publish]
                             ↓
                 +---------------------+
                 |   Pub/Sub Broker    |
                 +---------------------+
                        /        \
                       /          \
                Grupo Trad    Grupo IA
                 (2 agentes)   (2 agentes)
                    ↓              ↓
            Average Consensus   Average Consensus
                    \              /
                     \            /
                    +-------------+
                    | Whiteboard  |
                    +-------------+
                          |
                    +--------------+
                    | DecisionMaker|
                    +--------------+
```bash
## 📦 Requisitos

- Python 3.8+
- Pandas
- Scikit-learn
- Matplotlib
- Openpyxl

Instalación rápida:

```bash
pip install -r requirements.txt
