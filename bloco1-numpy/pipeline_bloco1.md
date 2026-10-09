# 🚁 Pipeline de Pré-processamento do Frame do Drone

> **IC-FAPEMA · Detecção de Capacetes em Motociclistas**
> 📘 Bloco 1 — NumPy

---

## 🗺️ Visão geral do fluxo

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│  1. FRAME BRUTO  │ ──▶ │  2. SLICING      │ ──▶ │  3. NORMALIZAÇÃO │ ──▶ │  4. ANOTAÇÕES    │
│  uint8 · 0–255   │     │  Canais + ROI    │     │  float32 · 0–1   │     │  YOLO            │
└──────────────────┘     └──────────────────┘     └──────────────────┘     └──────────────────┘
      Aula 1.1                 Aula 1.2                 Aula 1.3                 Aula 1.3
```

---

## 1️⃣ Frame Bruto do Drone

🏷️ **Aula 1.1**

### Criação

```python
import numpy as np

frame = np.random.randint(0, 256, size=(480, 640, 3), dtype=np.uint8)
```

### Características

| Propriedade | Valor |
|---|---|
| 🔢 **dtype** | `uint8` |
| 🎚️ **valores** | `0 → 255` |
| 📐 **shape** | `(480, 640, 3)` |

### Anatomia do `shape`

| Índice | Valor | Significado |
|:---:|:---:|---|
| `shape[0]` | **480** | ↕️ altura em pixels |
| `shape[1]` | **640** | ↔️ largura em pixels |
| `shape[2]` | **3** | 🎨 canais **R, G, B** |

---

## 2️⃣ Slicing — Canais e ROI

🏷️ **Aula 1.2**

### Separando os canais de cor

| Código | Resultado |
|---|---|
| `frame[:, :, 0]` | 🔴 canal **Vermelho** (R) |
| `frame[:, :, 1]` | 🟢 canal **Verde** (G) |
| `frame[:, :, 2]` | 🔵 canal **Azul** (B) |

### Recortando a ROI (Region of Interest)

| Código | Resultado |
|---|---|
| `frame[y1:y2, x1:x2]` | ✂️ recorte da ROI — **região do motociclista** |

```python
r = frame[:, :, 0]
g = frame[:, :, 1]
b = frame[:, :, 2]

roi = frame[y1:y2, x1:x2]
```

---

## 3️⃣ Normalização

🏷️ **Aula 1.3**

```python
# Passo 1 — converter o tipo
frame_float = frame.astype(np.float32)

# Passo 2 — escalar para 0.0–1.0
frame_norm = frame_float / 255.0
```

### Antes → Depois

| | Tipo | Faixa |
|---|:---:|:---:|
| ⬅️ **antes** | `uint8` | `0 – 255` |
| ➡️ **depois** | `float32` | `0.0 – 1.0` |

---

## 4️⃣ Anotações YOLO

🏷️ **Aula 1.3**

### Formato de cada linha

```
classe , x_centro , y_centro , largura_box , altura_box
```

| Coluna | Conteúdo | Faixa |
|:---:|---|:---:|
| `0` | 🏷️ classe do objeto | inteiro |
| `1` | 🎯 x_centro | 0.0 – 1.0 |
| `2` | 🎯 y_centro | 0.0 – 1.0 |
| `3` | 📏 largura_box | 0.0 – 1.0 |
| `4` | 📏 altura_box | 0.0 – 1.0 |

> 💡 Colunas **1–4** formam a bbox, todas normalizadas entre **0.0 e 1.0**.

### Extraindo com slicing

| Código | Resultado |
|---|---|
| `anotacoes[:, 0]` | extrai **todas as classes** |
| `anotacoes[:, 1:3]` | extrai os **centros (x, y)** |
| `anotacoes[:, 1:5]` | extrai as **bboxes completas** |

```python
classes = anotacoes[:, 0]
centros = anotacoes[:, 1:3]
bboxes  = anotacoes[:, 1:5]
```

---

## ✅ Saída pronta para o modelo

| Entrada | Formato |
|---|---|
| 🖼️ **frame normalizado** | `float32` · `0.0–1.0` |
| 🏷️ **anotações YOLO** | `[classe, x, y, w, h]` |

---

<sub>📌 IC-FAPEMA · Detecção de Capacetes em Motociclistas via Drone</sub>
