# 🔥 Classificação Binária da Presença de Fogo em Imagens com Yolov11
Este repositório tem por objetivo apresentar um projeto desenvolvido para a disciplina de graduação, Visão Computacional, que consiste em aborda uma solução para a classificação da presença de fogo em imagens usando o YOLOv11.

## 📌 Introdução
Em 2024, o Brasil registrou 278,3 mil focos de incêndio, segundo o Inpe, que representa um aumento de 46,5%, em relação ao ano anterior. De modo que a detecção precoce desses principios de incêndio é essencia para uma resposta rápida e eficaz, minimizando os danos causados. Para que isso aconteça é necessário um monitoramento automático de incêndio por meio de imagens. Nesse contexto, a aplicação de soluções baseadas em visão computacional e aprendizado de máquina tem se mostrado eficiente para a detecção precoce de focos de incêndio em imagens capturadas por satélites, câmeras fixas ou drones.

Este trabalho apresenta o desenvolvimento de um aplicação de classificação de imagens que identifica a presença ou ausência de fogo, utilizando a arquitetura YOLOv11, um modelo especifico para classificação de imagens. O objetivo é treinar esse modelo para classificar imagens em duas categorias: "fire" e "non_fire".

## ⚙️ Desenvolvimento / Técnicas Utilizadas
Para a tarefa de classificação de imagens, foi usado o dataset "Fire Dataset", disponiblizado no Kaggle, contendo 999 imagens categorizadas em duas pastas: `fire_images` e `non_fire_images`. O processo teve inicio com o download da base de dados, organizando-o da maneira como o YOLO aceita, é necessário que esteja organizado em subpastas de treinamento, validação e teste. Com isso, o conjunto de dados original extraídos do Kaggle foi dividio em três subconjuntos: treinamento (70%), validação (15%) e teste (15%). O gráfico mostra essa divisão.
<p align="center">
<img src="assets/distribution_dataset_img.png" alt="Gráfico de Distribuição das Imagens no Dataset" width="450"/>
</p>

A base de dados foi dividida nos conjuntos de treino, validação e teste da seguinte forma:

| Classe     | Treino | Validação | Teste |
|------------|--------|-----------|-------|
| `fire`     | 528    | 113       | 114   |
| `non_fire` | 170    | 36        | 38    |

Assim como, as imagens passaram por um processo de pré-processamento em que foram automaticamente redimensionadas para 640x640 pixels, conforme o parâmento `imgsz`, e normalizadas com valores de pixel convertidos para o intervalo `[0,1]`, conforme exigido pelo pipeline da Ultralytics. Além de técnicas leves de data augmentation foram aplicadas automaticamente, como espelhamento horizontal aleatório, corte e alterações no brilho e contraste, promovendo uma melhor capacidade de generalização do modelo.

Como modelo adotou-se a arquitetura Yolov11 na sua configuração pré-treinada voltada para a classificação de imagens (`yolo11n-cls.pt`). O treinamento foi conduzido por 25 épocas com batch size 16 e tendo como otimizador, o Adam. A principal métrica de desempenho utilizada foi a acurácia sobre os conjuntos de validação e teste.

Para realizar o treinamento, foi usado o ambiente de execução do Google Colab, com aceleração por GPU (Tesla T4)	 e a biblioteca PyTorch integrada à interface da Ultralytics.

## 📊 Resultados
Ao final do treinamento com o modelo YOLOv11, foram obtidos resultados satisfatórios quanto ao desempenho da aplicação com a taxa de erro residual minima. Conforme mostra a figura a seguir, é observado a evolução das curvas de loss e acurácia ao longo das épocas. E percebe-se que o **loss de treino** apresentou uma queda consistente e o de validação caiu rapidamente nas primeiras épocas, estabilizando-se próximo a zero. E em relação a **acurácia top-1**, teve uma evolução positiva, com valores superiores a 97%, e a **acurácia top-5** permaneceu constante em 100%.

<div align="center"> <img src="assets/train/results.png" alt="Curvas de Acurácia e Perda" width="400"/> </div>

Com isso, a acurácia do treinamento é 98,7%. Para avaliar o desempenho do modelo após o treinamento, foi fornecido a rede neural um conjunto de imagens testes, e obtido a matriz de confusão que demonstra a seguinte permformance.
<div align="center"> <img src="assets/test/confusion_matrix.png" alt="Matriz de Confusão" width="400"/> </div>

A partir dessa matriz nota-se que o modelo classificou corretamente 114 de 115 imagens da classe fire, e 36 das 38, non_fire. Isso demonstra uma acurácia de aproximadamente de 99,3%. Esses resultados indicam uma excelente capacidade de generalização para imagens nunca vistas. E considerando que a divisão do dataset foi aleatória, o modelo se mostrou robusto, com ótimo desempenho em detectar imagens com fogo mesmo em cenários variados de iluminação e perspectiva.

Notou-se um caso em que a rede erra na classificação a demonstrada abaixo.

## Conclusão
Os resultados alcançados foram possíveis devido a utilização do YOLOv11 na tarefa de classificação aliado ao otimizador Adam, permitindo encontrar um desempenho robusto sem a necessidade de arquiteturas complexas ou alto custo computacional. Em trabalhos futuros, pode-se expandir essa aplicação para a detecção localizada de focos de incêndio em tempo real (objeto + bounding box), incorporando variações climáticas e contextos diversos. 

