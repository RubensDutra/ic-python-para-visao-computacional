# 🐼 Pipeline Bloco 2 — Pandas

**Projeto:** IC-FAPEMA — Detecção de capacetes em motociclistas via drone

---

## 🗺️ Fluxo do Pipeline

```
Detecções do drone
       │
       ▼
┌─────────────────┐
│  pd.DataFrame() │  ← Organiza em tabela (linhas = detecções)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Inspecionar   │  ← shape / dtypes / head()
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│    Filtrar      │  ← df[condição] / loc / iloc
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│    Agrupar      │  ← groupby('frame').count()
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Estatísticas   │  ← groupby('classe').agg({'altura': ['mean','max']})
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Resumo Final   │  ← value_counts() / .sum()
└─────────────────┘
```

---

## 📖 Termos do Bloco

| Termo | Conceito | Função no código |
|---|---|---|
| **DataFrame** | Tabela com linhas e colunas | `pd.DataFrame({...})` |
| **Series** | Uma única coluna do DataFrame | `df['classe']` |
| **shape** | Dimensões da tabela (linhas, colunas) | `df.shape` |
| **dtypes** | Tipo de dado de cada coluna | `df.dtypes` |
| **head()** | Primeiras N linhas | `df.head(3)` |
| **filtro booleano** | Seleciona linhas por condição | `df[df['classe'] == 1]` |
| **loc** | Acessa linhas por rótulo/condição | `df.loc[df['x'] > 0.5]` |
| **iloc** | Acessa linhas por posição numérica | `df.iloc[0]` |
| **value_counts()** | Conta ocorrências por valor | `df['classe'].value_counts()` |
| **groupby()** | Agrupa linhas por valor de coluna | `df.groupby('classe')` |
| **mean()** | Média dos valores do grupo | `.mean()` |
| **count()** | Contagem de linhas por grupo | `.count()` |
| **agg()** | Várias estatísticas de uma vez | `.agg({'altura': ['mean','max']})` |

---

## 📂 Arquivos do Bloco

| Arquivo | Conteúdo |
|---|---|
| `aulas/aula_2_1_dataframes.ipynb` | DataFrame, Series, shape, dtypes |
| `aulas/aula_2_2_filtragem.ipynb` | head(), filtro booleano, loc, iloc, value_counts() |
| `aulas/aula_2_3_agrupamentos.ipynb` | groupby(), mean(), count(), agg() |
| `exercicios/ex_2_1_dataframes.ipynb` | Exercício DataFrame voo_01 |
| `exercicios/ex_2_2_filtragem.ipynb` | Exercício filtragem de detecções |
| `exercicios/ex_2_3_agrupamentos.ipynb` | Exercício agrupamentos e estatísticas |
| `projeto_integrador_bloco2.ipynb` | Pipeline completo Bloco 2 |

---

## 🔗 Conexão com o projeto real

> No projeto de detecção de capacetes, o YOLO gera um arquivo `.txt` por frame com todas as detecções. O Pandas transforma essas detecções em DataFrame para análise: filtrar infratores, calcular taxa de não-conformidade e identificar regiões críticas no frame.
