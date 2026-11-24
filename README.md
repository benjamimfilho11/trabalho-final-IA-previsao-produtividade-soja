
# Previsão da Produtividade da Soja no Brasil

**Projeto Final — Inteligência Artificial | Universidade Federal do Piauí (UFPI) | 2026**

Estudo comparativo de **Regressão Linear** e **Perceptron Multicamadas (MLP)** para estimar a produtividade municipal da soja no Brasil a partir de registros históricos do IBGE/PAM e de variáveis climáticas da NASA POWER.

## Materiais do projeto

| Material | Acesso |
| --- | --- |
| Artigo científico (Overleaf) | [Abrir artigo](https://www.overleaf.com/project/6b004fedb41cc5c7837d806e/share#831ccf075d91c7c51adc42f109cf973dc052dd0fb27543f2) |
| Notebook e experimentos (Google Colab) | [Abrir notebook](https://colab.research.google.com/drive/1f_eniJZymZAiHi0WjtnyhFEiTp9dgnrJ?usp=sharing) |
| Dados e arquivos complementares (Google Drive) | [Abrir pasta](https://drive.google.com/drive/folders/1ovhSAwAruHJj-w68PqG7Sj_iLgRKQzRq) |
| Apresentação (Canva) | [Abrir apresentação](https://canva.link/9ixejre43aq11y9) |

## Resumo

O projeto investiga o desempenho de dois métodos de aprendizado supervisionado na estimativa da produtividade da soja em municípios brasileiros, utilizando informações climáticas e registros históricos de produção agrícola.

O objetivo é avaliar se a maior complexidade de uma rede neural MLP proporciona vantagens relevantes em relação à Regressão Linear.

### Dados e atributos

- **Base final:** 49.490 observações município-ano, de 2001 a 2025.
- **Abrangência:** municípios produtores de soja no Brasil.
- **Dados agrícolas:** IBGE — Produção Agrícola Municipal (PAM).
- **Dados climáticos:** NASA POWER.
- **Variáveis preditoras:** temperatura média, temperatura máxima, umidade relativa, precipitação, radiação solar, ano agrícola e produtividade do ano anterior.
- **Variável-alvo:** produtividade da soja em kg/ha.

As variáveis climáticas foram agregadas considerando uma janela de setembro a março, representando uma aproximação do período de cultivo.

### Modelos utilizados

Foram avaliados:

- Regressão Linear.
- MLP com uma camada oculta de 16 neurônios.
- MLP com duas camadas ocultas de 32 e 16 neurônios.
- MLP com duas camadas ocultas de 64 e 32 neurônios.

A arquitetura selecionada foi utilizada em um **ensemble de 10 redes MLP**, treinadas com diferentes sementes aleatórias, cujas previsões foram combinadas por média.

### Protocolo experimental

Para respeitar a natureza temporal dos dados, foi adotada uma divisão cronológica:

| Conjunto | Período | Observações |
| --- | --- | ---: |
| Treinamento | 2001–2019 | 34.679 |
| Validação | 2020–2022 | 7.145 |
| Teste | 2023–2025 | 7.666 |

A avaliação utilizou as métricas **MAE**, **RMSE** e **R²**, além de dois baselines históricos:

1. Produtividade observada no ano anterior.
2. Média histórica municipal dos anos anteriores.

## Resultados

### Desempenho no conjunto de teste (2023–2025)

| Abordagem | MAE (kg/ha) | RMSE (kg/ha) | R² |
| --- | ---: | ---: | ---: |
| Produtividade do ano anterior | 603,26 | 878,40 | -0,399 |
| Média histórica municipal | 602,49 | 733,14 | 0,025 |
| Regressão Linear | 497,98 | **648,85** | **0,236** |
| MLP Ensemble | **490,96** | 651,54 | 0,230 |

O ensemble MLP apresentou o menor MAE, com uma melhoria aproximada de **1,41% em relação à Regressão Linear**.

Entretanto, a Regressão Linear alcançou resultados ligeiramente superiores em RMSE e R².

Ambos os modelos superaram os baselines históricos, com reduções de aproximadamente **17% a 19% no MAE**.

### Análise dos resultados

A comparação revelou que:

- A MLP apresentou o menor MAE global.
- A Regressão Linear foi competitiva, apesar de sua menor complexidade.
- O desempenho relativo dos modelos variou entre 2023, 2024 e 2025.
- Os maiores erros ocorreram em faixas de produtividade extremamente baixas ou elevadas.
- As informações históricas de produtividade contribuíram significativamente para o desempenho dos modelos.

Os resultados indicam que o aumento da complexidade do modelo não garante melhorias consistentes em todas as métricas e condições de avaliação.

## Limitações

O estudo utiliza informações climáticas observadas durante a janela completa de cultivo. Portanto, a abordagem representa uma estimativa da produtividade a partir de dados da safra, não uma previsão antecipada antes do plantio.

Outras limitações incluem a ausência de variáveis relacionadas ao solo, índices de vegetação e determinadas condições de manejo agrícola.

Como trabalhos futuros, podem ser investigadas novas fontes de dados, estratégias de previsão antecipada e avaliações em diferentes contextos regionais.

## Tecnologias utilizadas

- Python
- Google Colab / Jupyter Notebook
- Pandas e NumPy
- Scikit-learn
- Matplotlib

## Fontes de dados

- [IBGE/PAM — Tabela 1612](https://sidra.ibge.gov.br/tabela/1612)
- [NASA POWER](https://power.larc.nasa.gov/data-access-viewer/)
- [Municípios Brasileiros — GitHub](https://github.com/kelvins/Municipios-Brasileiros)

## Documentação

O desenvolvimento completo, incluindo preparação dos dados, análise exploratória, implementação dos modelos, experimentos, gráficos e interpretação dos resultados, está documentado no [notebook do Google Colab](https://colab.research.google.com/drive/1f_eniJZymZAiHi0WjtnyhFEiTp9dgnrJ?usp=sharing).

O artigo científico e a apresentação estão disponíveis nos links apresentados no início deste README.

---

**Projeto desenvolvido para a disciplina de Inteligência Artificial — Universidade Federal do Piauí (UFPI), 2026.**
