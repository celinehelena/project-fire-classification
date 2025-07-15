# 🔥 Classificação Binária da Presença de Fogo em Imagens com Yolov11
Este repositório tem por objetivo apresentar um projeto desenvolvido para a disciplina de graduação, Visão Computacional, que consiste em aborda uma solução para a classificação da presença de fogo em imagens usando o YOLOv11.

## 📌 Introdução
Em 2024, o Brasil registrou 278,3 mil focos de incêndio, segundo o Inpe, que representa um aumento de 46,5%, em relação ao ano anterior. De modo que a detecção precoce desses principios de incêndio é essencia para uma resposta rápida e eficaz, minimizando os danos causados. Para que isso aconteça é necessário um monitoramento automático de incêndio por meio de imagens. Nesse contexto, a aplicação de soluções baseadas em visão computacional e aprendizado de máquina tem se mostrado eficiente para a detecção precoce de focos de incêndio em imagens capturadas por satélites, câmeras fixas ou drones.

Este trabalho apresenta o desenvolvimento de um aplicação de classificação de imagens que identifica a presença ou ausência de fogo, utilizando a arquitetura YOLOv11, um modelo especifico para classificação de imagens. O objetivo é treinar esse modelo para classificar imagens em duas categorias: "fire" e "non_fire".

## ⚙️ Desenvolvimento / Técnicas Utilizadas
Para a tarefa de classificação de imagens, foi usado o dataset "Fire Dataset", disponiblizado no Kaggle, contendo 999 imagens categorizadas em duas pastas: fire_images e non_fire_images. O processo teve inicio com o download da base de dados, organizando-o da maneira como o Yolo aceita, é necessário que esteja organizado em subpastas de treinamento, validação e teste. Com isso, o conjunto de dados original extraídos do Kaggle foi dividio em três subconjuntos: treinamento (70%), validação (15%) e teste (15%). O gráfico mostra essa divisão.

Assim como, as imagens passaram por um processo de pré-processamento em que foram automaticamente redimensionadas para 640x640 pixels, conforme o parâmento imgsz, e normalizadas com valores de pixel convertidos para o intervalo [0,1], conforme exigido pelo pipeline da Ultralytics. Além de técnicas leves de data augmentation foram aplicadas automaticamente, como espelhamento horizontal aleatório, corte e alterações no brilho e contraste, promovendo uma melhor capacidade de generalização do modelo.

Como modelo adotou-se a arquitetura Yolov11 na sua configuração pré-treinada voltada para a classificação de imagens (yolo11n-cls.pt). O treinamento foi conduzido por 25 épocas com batch size 16 e tendo como otimizador, o Adam. A principal métrica de desempenho utilizada foi a acurácia sobre os conjuntos de validação e teste.

Para realizar o treinamento, foi usado o ambiente de execução do Google Colab, com aceleração por GPU(Tesla T4)	 e a biblioteca PyTorch integrada à interface da Ultralytics.
