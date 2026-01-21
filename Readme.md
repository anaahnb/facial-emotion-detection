# Aplicação de detecção de emoções em tempo real

Este projeto consiste em uma aplicação web desenvolvida para detectar emoções humanas em tempo real a partir de vídeo, utilizando técnicas de processamento de imagens e aprendizado de máquina.

A aplicação é capaz de reconhecer as seguintes emoções faciais:

- Raiva
- Desprezo
- Felicidade
- Neutro
- Tristeza
- Surpresa

## Tecnologias utilizadas
- HTML5
- Python 3
- TensorFlow.js
- BlazeFace
- MobileNet
- Web API


## Arquitetura

O projeto foi estruturado de forma a separar claramente as etapas de treinamento do modelo e inferência em tempo real, seguindo boas práticas de aprendizado de máquina e engenharia de software.

```
Treinamento (Python) → Exportação para TensorFlow.js → Inferência (Browser)
```


###  Camadas da Arquitetura

* **Treinamento**

  * Responsável pelo treinamento da rede neural convolucional baseada em **MobileNetV2**
  * Avaliação do modelo por meio de métricas e matriz de confusão
  * Conversão do modelo treinado para o formato compatível com TensorFlow.js

* **Inferência**

  * Captura de vídeo em tempo real via webcam
  * Detecção de rostos utilizando BlazeFace
  * Classificação das emoções diretamente no navegador com TensorFlow.js

## Treinamento do Modelo

O modelo de classificação de emoções foi treinado previamente em ambiente Python, utilizando bibliotecas de aprendizado de máquina e deep learning.

### Etapas do Treinamento

1. **Aquisição do Dataset**

   * Conjunto de imagens faciais rotuladas por emoção

2. **Pré-processamento**

   * Redimensionamento das imagens
   * Normalização dos pixels
   * Conversão para escala compatível com o modelo

3. **Extração de Características**

   * Uso da arquitetura **MobileNet** como base (transfer learning)

4. **Treinamento da Rede Neural**

   * Ajuste dos pesos para classificação das emoções

5. **Avaliação do Modelo**

   * Cálculo de métricas de desempenho

6. **Exportação para TensorFlow.js**

   * Conversão do modelo treinado para o formato `model.json` + arquivos `.bin`


## Avaliação do modelo

A matriz de confusão foi utilizada para avaliar o desempenho do modelo de classificação de emoções.

![Matriz de confusão](./training/plots/confusion_matrix.png)

A partir da matriz, é possível observar:
* A taxa de acertos por classe
* Emoções com maior confusão entre si
* Pontos fortes e limitações do modelo

---

O gráfico abaixo apresenta a evolução da acurácia (accuracy) e da função de perda (loss) do modelo ao longo das épocas de treinamento.

![Histórico de Treinamento do Modelo](./training/plots/training_history.png)

A partir do gráfico, é possível observar a convergência do modelo durante o treinamento, indicando aprendizado progressivo e estabilidade nas métricas avaliadas.


## Estrutura de Pastas e Arquivos

```
facial-emotion-detection/
├── src/
│   └── web/                     # Aplicação web (TensorFlow.js)
│       ├── index.html           # Página principal
│       ├── script.js            # Lógica de captura e inferência
│       ├── EmotionDetectorFactory.js
│       ├── tf.min.js            # TensorFlow.js
│       ├── blazeface/           # Detecção de rostos
│       └── model/               # Modelo treinado
│           ├── model.json
│           ├── group1-shard*.bin
│           └── mobilenet/
│
├── training/                    # Treinamento do modelo (Python)
│   ├── train_mobilenetv2.py     # Script de treinamento
│   ├── convert_mobilenetv2.py   # Conversão para TensorFlow.js
│   └── plots/                   # Resultados experimentais
│       ├── confusion_matrix.png
│       └── accuracy_loss.png
│
└── README.md                    # Documentação do projeto

```

Os scripts em `training/` documentam o processo de treinamento e avaliação do modelo, enquanto a pasta `src/web/` contém exclusivamente a aplicação final executada no navegador.


## Como executar a aplicação

A aplicação pode ser acessada via navegador clicando [aqui](https://facial-emotion-detection-e9vn.vercel.app/)


### Executar localmente

#### 1. Clonar o repositório

```bash
git clone https://github.com/<usuario>/<repositorio>.git
cd <repositorio>
```

#### 2. Subir um servidor local


```bash
python3 -m http.server 8000
```

#### Acessar no navegador

```
http://localhost:8000/src/web/
```


---


Ao entrar no site, **clique em "Start Camera"**, espere alguns segundos até que o modelo conclua o carregamento e **permita o acesso a câmera através de um pop-up que aparecerá no navegador**

![Demonstração do pop-up](./src/web/assets/popup.png)

<small>Demonstração de um pop-up de permissão</small>

