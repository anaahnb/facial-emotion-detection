# Aplicação de detecção de emoções em tempo real

Este projeto consiste em uma aplicação web capaz de detectar emoções humanas em tempo real a partir de vídeo.

## Tecnologias utilizadas
- HTML5
- Python 3
- TensorFlow.js
- BlazeFace
- MobileNet
- Web API


## Arquitetura

A arquitetura do sistema segue o modelo Client-Side Machine Learning, conforme ilustrado abaixo:


```
Câmera do Usuário
        ↓
Captura de Frames (Web API - getUserMedia)
        ↓
Detecção de Rosto (BlazeFace)
        ↓
Pré-processamento da Imagem
        ↓
Classificação de Emoções (TensorFlow.js)
        ↓
Exibição do Resultado em Tempo Real
```


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

![Matriz de confusão](./plots/confusion_matrix.png)

A partir da matriz, é possível observar:

* A taxa de acertos por classe
* Emoções com maior confusão entre si
* Pontos fortes e limitações do modelo


## Estrutura de Pastas e Arquivos

```
project-root/
├── index.html                 # Página principal da aplicação
├── script.js                  # Lógica principal (captura de vídeo e inferência)
├── EmotionDetectorFactory.js  # Fábrica do detector de emoções
├── tf.min.js                  # TensorFlow.js
├── blazeface/                 # Biblioteca de detecção de rostos
├── model/                     # Modelo treinado
│   ├── model.json             # Arquitetura do modelo
│   ├── group1-shard*.bin      # Pesos do modelo
│   └── mobilenet/             # Pesos da MobileNet
└── README.md                  # Documentação do projeto
```


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
