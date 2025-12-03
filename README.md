# Predição de Performance de Criativos usando CNN

_"Tecnicamente, é um dos trabalhos mais sofisticados, utilizando Deep Learning e Transfer Learning aplicados a imagens. A ideia de prever performance de marketing com base na imagem do produto é excelente. O R² negativo no teste indica que o modelo falhou em generalizar (provavelmente poucos dados para a complexidade da rede), mas a tentativa é válida academicamente."_  
**- FELIPE ALBINO DOS SANTOS**  

Este projeto foi desenvolvido como requisito da disciplina **Projeto Aplicado II** do curso de **Ciência de Dados** na **Universidade Presbiteriana Makenzie**. 

## Descrição

Este projeto tem como objetivo desenvolver um modelo que prevê a performance de publicações pagas em redes sociais, utilizando análise de imagens dos criativos e dados históricos de campanhas anteriores, para treinar uma rede neural convolucional sequencial que seja capaz de prever a performance de imagens em redes sociais, antes mesmo de suas publicações.

## O Produto

Suponha a seguinte situação:  
Uma agência publicitária tem um contrato mensal (retainer) que o fornece uma quantidade de material criativo maior do que será publicado. É necessário fazer uma seleção e aprovação de parte desse material, e é aqui que o modelo cumpre seu papel, prevendo o resultado de cada peça de acordo com padrões apreendidos de publicações passadas.

## Ensaio e desafios

O Stakeholder dispôs um total de 35 imagens, algumas das quais eram thumbnails de vídeos, e esse foi todo o material disponível para o treinamento do modelo. É sabido que redes destinadas à visão computacional são treinadas com algumas dezenas de milhares de imagens; entretando, ainda foi válido o desenvolvimento do projeto, já que o pipeline está adaptado para receber qualquer dataset como treinamento.

## Resultados

O relatório completo, incluindo EDA, estudo teórico do funcionamento da CNN e resultados pormenorizados podem ser encontrados em `reports/Relatório Técnico FINAL Projeto Aplicado II_A4.pdf`.

Durante o desenvolvimento do pipeline e sucessivo treinamento da rede, havia a suposição de que um número amostral tão baixo e com técnicas refinadas de seleção de hiperparâmetros e validação fariam com que o modelo não generalizasse o suficiente, mas o resultado foi ainda pior. Reportamos $R² = -0.0176$, o que significa que considerar sempre a média da amostra como resposta para toda e qualquer imagem traria menos erros (totais absolutos) do que o modelo alcançou.

O modelo mostrou-se enviesado, tentendo a prever resultados em torno de 100 e 200 CTR, como mostra a distribuição de predições e valores reais abaixo:

<img width="489" height="390" alt="predito_vs_real" src="https://github.com/user-attachments/assets/db1bbdc7-f276-4e20-894d-f65489b31d08" />

Os gráficos abaixo mostram o erro absoluto médio de trieno e teste ao longo das épocas para cada fold de uma combinação de hiperparâmetros para o LOOCV. Os padrões observados reforçam a avaliação acima:

<img width="1589" height="2690" alt="val_folds" src="https://github.com/user-attachments/assets/43429d5f-f505-422e-853b-e4f7832f1e25" />

Com o poder computacional de que dispomos, apenas 5 tentativas foram concluídas durante o Random Search, e acreditamos que mais tentativas levará ao cenário esperado para uma amostra tão pequena.

Estamos esperançosos por tentar o algoritmo em uma máquina com maior capacidade de processamento e maior base de treino. Não descartamos, porém, a hipótese de que as imagens não sejam mesmo determinantes para a performance de sua publicação.

## Etapas do Projeto

Este projeto é dividido em 5 etapas:
* Arquitetura da CNN
* Validação cruzada (LOOCV)
* Busca aleatória de hiperparâmetros (Random Search)
* Modelo definitivo
* Avaliação do modelo

O processamento de todas as etapas pode ser acompanhado executando os notebooks (.ipynb) na raiz do repositório. As três primeiras etapas estão em `Transfer_learning_and_fine_tuning.ipynb`; o modelo definitivo é obtido em `best_fit_as_product.ipynb`; e a avaliação do modelo está em `model_evaluation.ipynb`. O notebook `update_images_path.ipynb` foi utilizado para adequar os diretórios das imagens durante a montagem do dataset.

## Como reproduzir
1. Clone ou baixe este repositório em um diretório apropriado.
2. Crie um ambiente Python e instale as dependências listadas em `requirements.txt`.
3. Execute integralmente o notebook `Transfer_learning_and_fine_tuning.ipynb` antes de executar `model_evaluation.ipynb` e `best_fit_as_product.ipynb`; estes dois últimos são independentes entre si.

## Estrutura do Projeto

ProjetoII  
 │  
 ├── data/  
 │ ├── raw/                  # Dados brutos, imagens originais e metadados não processados  
 │ │ ├── for_fit/            # Dados para treino e teste do modelo  
 │ │ └── for_predict/        # Imagens a serem previstas  
 │ └── processed/            # Dados pré-processados prontos para uso (matrizes, features)   
 │  
 ├── src/                    # Código-fonte do projeto  
 │ ├── data_preprocessing/   # Scripts para carregamento e limpeza dos dados, pré-processamento de imagens  
 │ ├── feature_extraction/   # Scripts para extração de features visuais e textuais  
 │ ├── models/               # Definição e treinamento dos modelos de deep learning  
 │ ├── evaluation/           # Scripts para avaliação de métricas e análise dos  
 │ │	resultados  
 │ ├── utils/                # Funções utilitárias e helpers gerais  
 │ └── inference/            # Código para gerar predições com modelos treinados   
 │  
 ├── reports/                # Documentação do projeto, relatórios e apresentações  
 │  
 ├── requirements.txt        # Lista de dependências necessárias para rodar o projeto  
 ├── README.md               # Apresentação do projeto e instruções principais  
 └── .gitignore              # Arquivos e pastas ignorados pelo Git  

## Dependências

- Python 3.11+
- TensorFlow
- pandas, numpy, scikit-learn
- OpenCV ou PIL para processamento de imagens
- Jupyter para notebooks

## Autores

- Felipe Neres Silva Bezerra
- Guilherme Da Silva Brevilato
- Isabela Kazue Sinoduka
- Pedro Henrique Bittencourt De Freitas 
