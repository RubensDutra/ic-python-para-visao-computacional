Bloco 1 — NumPy

# Pipeline de Pré-processamento do Frame do Drone

IC-FAPEMA · Detecção de Capacetes em Motociclistas

1

Frame Bruto do Drone

Aula 1.1

Criação np.random.randint(0, 256, size=(480, 640, 3), dtype=np.uint8)

dtype: uint8 valores: 0 → 255 shape: (480, 640, 3)

| shape\[0\] = 480 | altura em pixels |
| --- | --- |
| shape\[1\] = 640 | largura em pixels |
| shape\[2\] = 3 | canais R, G, B |

2

Slicing — Canais e ROI

Aula 1.2

| frame\[:, :, 0\] | canal Vermelho (R) |
| --- | --- |
| frame\[:, :, 1\] | canal Verde (G) |
| frame\[:, :, 2\] | canal Azul (B) |
| frame\[y1:y2, x1:x2\] | recorte da ROI — região do motociclista |

3

Normalização

Aula 1.3

Passo 1 frame.astype(np.float32)

Passo 2 frame_float / 255.0

antes: uint8 · 0–255 depois: float32 · 0.0–1.0

4

Anotações YOLO

Aula 1.3

classe , x_centro , y_centro , largura_box , altura_box

coluna 0 — classe do objeto

colunas 1–4 — bbox (todos 0.0–1.0)

| anotacoes\[:, 0\] | extrai todas as classes |
| --- | --- |
| anotacoes\[:, 1:3\] | extrai centros (x, y) |
| anotacoes\[:, 1:5\] | extrai bboxes completas |

✓ Saída pronta para o modelo

frame normalizado + anotações YOLO

float32 · 0.0–1.0 · \[classe, x, y, w, h\]