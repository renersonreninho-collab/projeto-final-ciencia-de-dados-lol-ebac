# Projeto Final EBAC - Previsão de Partidas de League of Legends

Projeto final do curso de **Ciência de Dados da EBAC**. O objetivo é prever se o **Blue Team** vencerá uma partida de League of Legends a partir do estado do jogo aos 10 minutos.

## Acesso rápido

- [Ver o notebook completo](notebooks/Projeto_Final_LoL_EBAC.ipynb)
- [Ver a apresentação final em PDF](presentation/Apresentacao_Projeto_Final_LoL_EBAC.pdf)
- [Acessar a base de dados](data/Base_M43_Pratique_LOL_RANKED_WIN.csv)

## Resultado principal

O modelo final foi uma **Regressão Logística com padronização**, selecionada por validação cruzada e ajustada com `GridSearchCV` (`C = 0.03`). No conjunto de teste reservado, obteve:

| Métrica | Resultado |
|---|---:|
| Accuracy | 71.66% |
| Precision | 71.17% |
| Recall | 72.62% |
| F1-score | 71.89% |
| ROC-AUC | 0.8060 |
| Log Loss | 0.5313 |

Matriz de confusão: `[[700, 290], [270, 716]]`.

## Metodologia

1. Entendimento do problema e auditoria da base.
2. Análise exploratória e verificação de qualidade.
3. Identificação de redundâncias matemáticas entre features.
4. Análise de ouro, experiência, First Blood, dragões, arautos e torres.
5. Testes estatísticos.
6. Split estratificado treino/teste, mantendo o teste fechado durante a seleção.
7. Baseline e comparação de Regressão Logística, Decision Tree, Random Forest e SVM Linear com validação cruzada.
8. Tuning da Regressão Logística com `GridSearchCV`.
9. Avaliação única no conjunto de teste reservado.
10. Interpretação dos coeficientes, confiança das previsões, limitações e conclusões.

## Principais insights

- Vantagem de ouro e experiência no early game estão entre os sinais preditivos mais relevantes.
- Objetivos como dragão também acrescentam informação ao modelo.
- Em 725 partidas nas quais o modelo apresentou pelo menos 80% de confiança para um dos lados, a acurácia foi de aproximadamente **89.1%**.
- Em partidas equilibradas, com probabilidade prevista para Blue entre 40% e 60%, a acurácia caiu para aproximadamente **53.7%**, evidenciando maior incerteza.
- As relações encontradas são preditivas/associativas e não devem ser interpretadas automaticamente como causalidade.

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- SciPy
- Scikit-learn
- Jupyter Notebook
- Git e GitHub

## Estrutura do repositório

```text
projeto-final-ciencia-de-dados-lol-ebac/
├── data/
│   └── Base_M43_Pratique_LOL_RANKED_WIN.csv
├── notebooks/
│   └── Projeto_Final_LoL_EBAC.ipynb
├── presentation/
│   └── Apresentacao_Projeto_Final_LoL_EBAC.pdf
├── README.md
└── requirements.txt
```

## Como reproduzir

Clone o repositório e instale as dependências:

```bash
pip install -r requirements.txt
```

Em seguida, abra:

```text
notebooks/Projeto_Final_LoL_EBAC.ipynb
```

O notebook procura automaticamente a base em `../data/` quando executado a partir da pasta `notebooks`.

## Limitações

A base representa um recorte específico de partidas e não inclui todas as informações que poderiam afetar o resultado, como composição completa de campeões, habilidade individual, histórico dos jogadores ou a evolução temporal depois do snapshot. Mudanças de patch/meta podem gerar drift e exigiriam revalidação em um uso de produção.

## Arquivos de entrega

- `Projeto_Final_LoL_EBAC.ipynb`: análise técnica reproduzível.
- `Apresentacao_Projeto_Final_LoL_EBAC.pdf`: apresentação executiva do projeto.
- `Base_M43_Pratique_LOL_RANKED_WIN.csv`: base utilizada.
