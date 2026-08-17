# Projeto Final EBAC - Previsao de Partidas de League of Legends

Projeto final do curso de Ciencia de Dados da EBAC. O objetivo e prever se o **Blue Team** vencera uma partida de League of Legends a partir do estado do jogo aos 10 minutos.

## Resultado principal

O modelo final foi uma **Regressao Logistica com padronizacao**, selecionada por validacao cruzada e ajustada com `GridSearchCV` (`C = 0.03`). No conjunto de teste reservado, obteve:

| Metrica | Resultado |
|---|---:|
| Accuracy | 71.66% |
| Precision | 71.17% |
| Recall | 72.62% |
| F1-score | 71.89% |
| ROC-AUC | 0.8060 |
| Log Loss | 0.5313 |

Matriz de confusao: `[[700, 290], [270, 716]]`.

## Metodologia

1. Entendimento do problema e auditoria da base.
2. Analise exploratoria e verificacao de qualidade.
3. Identificacao de redundancias matematicas entre features.
4. Analise de ouro, experiencia, First Blood, dragoes, arautos e torres.
5. Testes estatisticos.
6. Split estratificado treino/teste, mantendo o teste fechado durante selecao.
7. Baseline e comparacao de Regressao Logistica, Decision Tree, Random Forest e SVM Linear com validacao cruzada.
8. Tuning da Regressao Logistica com `GridSearchCV`.
9. Avaliacao unica no conjunto de teste reservado.
10. Interpretacao dos coeficientes, confianca das previsoes, limitacoes e conclusoes.

## Principais insights

- Vantagem de ouro e experiencia no early game estao entre os sinais preditivos mais relevantes.
- Objetivos como dragao tambem acrescentam informacao ao modelo.
- Em 725 partidas nas quais o modelo apresentou pelo menos 80% de confianca para um dos lados, a acuracia foi de aproximadamente **89.1%**.
- Em partidas equilibradas, com probabilidade prevista para Blue entre 40% e 60%, a acuracia caiu para aproximadamente **53.7%**, evidenciando maior incerteza.
- As relacoes encontradas sao preditivas/associativas e nao devem ser interpretadas automaticamente como causalidade.

## Estrutura sugerida do repositorio

```text
projeto-final-lol-ebac/
|-- README.md
|-- requirements.txt
|-- data/
|   `-- Base_M43_Pratique_LOL_RANKED_WIN.csv
|-- notebooks/
|   `-- Projeto_Final_LoL_EBAC.ipynb
`-- presentation/
    `-- Apresentacao_Projeto_Final_LoL_EBAC.pdf
```

## Como executar

Crie um ambiente Python, instale as dependencias e abra o notebook em Jupyter Notebook, JupyterLab, VS Code ou Google Colab.

```bash
pip install -r requirements.txt
```

O notebook procura o CSV na pasta atual, em `../data/` e no caminho usado durante a geracao do projeto. Para o repositorio GitHub, mantenha o notebook em `notebooks/` e o CSV em `data/`.

## Limitacoes

A base representa um recorte especifico de partidas e nao inclui todas as informacoes que poderiam afetar o resultado, como composicao completa de campeoes, habilidade individual, historico dos jogadores ou a evolucao temporal depois do snapshot. Mudancas de patch/meta podem gerar drift e exigiriam revalidacao em um uso de producao.

## Arquivos de entrega

- `Projeto_Final_LoL_EBAC.ipynb`: analise tecnica reproduzivel.
- `Apresentacao_Projeto_Final_LoL_EBAC.pdf`: apresentacao executiva do projeto.
- `Base_M43_Pratique_LOL_RANKED_WIN.csv`: base utilizada.
