# 🔥 Classificação Binária da Presença de Fogo em Imagens com Yolov11
Este repositório tem por objetivo apresentar um projeto desenvolvido para a disciplina de graduação, Visão Computacional, que consiste em aborda uma solução para a classificação da presença de fogo em imagens usando o YOLOv11.

## 📌 Introdução
Em 2024, o Brasil registrou 278,3 mil focos de incêndio, segundo o Inpe, que representa um aumento de 46,5%, em relação ao ano anterior. De modo que a detecção precoce desses principios de incêndio é essencia para uma resposta rápida e eficaz, minimizando os danos causados. Para que isso aconteça é necessário um monitoramento automático de incêndio por meio de imagens. Nesse contexto, a aplicação de soluções baseadas em visão computacional e aprendizado de máquina tem se mostrado eficiente para a detecção precoce de focos de incêndio em imagens capturadas por satélites, câmeras fixas ou drones.

Este trabalho apresenta o desenvolvimento de um aplicação de classificação de imagens que identifica a presença ou ausência de fogo, utilizando a arquitetura YOLOv11, um modelo especifico para classificação de imagens. O objetivo é treinar esse modelo para classificar imagens em duas categorias: "fire" e "non_fire".

## ⚙️ Desenvolvimento / Técnicas Utilizadas
Para a tarefa de classificação de imagens, foi utilizado o Fire Dataset, disponibilizado no Kaggle, contendo 999 imagens organizadas em duas categorias: `fire_images` e `non_fire_images`. O processo teve início com o download da base de dados e sua reorganização no formato exigido pelo YOLO, com as imagens distribuídas em subpastas para treinamento, validação e teste. O conjunto original foi, então, dividido aleatoriamente em três subconjuntos: treinamento (70%), validação (15%) e teste (15%). O gráfico abaixo ilustra essa divisão:
<p align="center">
<img src="assets/distribution_dataset_img.png" alt="Gráfico de Distribuição das Imagens no Dataset" width="450"/>
</p>

A divisão foi realizada com auxílio de um script que aloca aleatoriamente as imagens entre os três subconjuntos. A distribuição final das imagens ficou da seguinte forma:

| Classe     | Treino | Validação | Teste |
|------------|--------|-----------|-------|
| `fire`     | 528    | 113       | 114   |
| `non_fire` | 170    | 36        | 38    |

As imagens passaram por um processo de pré-processamento, sendo automaticamente redimensionadas para 640×640 pixels, conforme o parâmetro `imgsz`, e normalizadas com os valores de pixel convertidos para o intervalo `[0, 1]`, como exigido pelo pipeline da Ultralytics. Técnicas leves de data augmentation foram aplicadas automaticamente, incluindo espelhamento horizontal aleatório, corte e alterações de brilho e contraste, contribuindo para uma melhor capacidade de generalização do modelo.

O modelo utilizado foi a arquitetura YOLOv11, na versão pré-treinada para tarefas de classificação (`yolo11n-cls.pt`). O treinamento foi conduzido por 25 épocas, com batch size 16 e uso do otimizador `Adam`. A principal métrica de desempenho adotada foi a acurácia nos conjuntos de validação e teste.

O treinamento foi realizado no ambiente Google Colab, com aceleração por GPU (Tesla T4), utilizando a biblioteca PyTorch integrada à interface da Ultralytics.

## 📊 Resultados
Ao final do treinamento, o modelo **YOLOv11** apresentou desempenho satisfatório, com taxa de erro residual mínima. A figura a seguir mostra a evolução das curvas de loss e acurácia ao longo das épocas. Nota-se que o **loss** de treino teve uma queda consistente, enquanto o de validação caiu rapidamente nas primeiras épocas e estabilizou-se próximo de zero. Já a **acurácia top-1** evoluiu positivamente, superando 97%, enquanto a **acurácia top-5** manteve-se constante em 100%.

<div align="center"> <img src="assets/train/results.png" alt="Curvas de Acurácia e Perda" width="400"/> </div>

A acurácia final no conjunto de treinamento foi de **98,7%**. Para avaliar o desempenho após o treinamento, a rede foi testada com o conjunto de teste, e a matriz de confusão obtida demonstra a seguinte performance:
<div align="center"> <img src="assets/test/confusion_matrix.png" alt="Matriz de Confusão" width="400"/> </div>

A partir da matriz, observa-se que o modelo classificou corretamente 114 de 115 imagens da classe `fire` e 36 de 38 da classe `non_fire`, o que corresponde a uma acurácia de aproximadamente **99,3%**. Esses resultados indicam uma excelente capacidade de generalização para imagens não vistas anteriormente. Considerando a divisão aleatória do dataset, o modelo mostrou-se robusto, com ótimo desempenho mesmo em cenários variados de iluminação e perspectiva.

A seguir, é apresentada uma imagem com alguns dos resultados de classificação do modelo:
<div align="center"> <img src="assets/test/confusion_matrix.png" alt="Matriz de Confusão" width="400"/> </div>
Foi identificado apenas um caso de erro de classificação, ilustrado na imagem abaixo.

## Conclusão
Os resultados alcançados foram possíveis devido a utilização do YOLOv11 na tarefa de classificação aliado ao otimizador Adam, permitindo encontrar um desempenho robusto sem a necessidade de arquiteturas complexas ou alto custo computacional. Em trabalhos futuros, pode-se expandir essa aplicação para a detecção localizada de focos de incêndio em tempo real (objeto + bounding box), incorporando variações climáticas e contextos diversos. 

