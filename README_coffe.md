# Classificação de Grãos de Café por Textura: GLCM (Haralick) + Classificadores Clássicos

**Disciplina:** Processamento de Imagens – UTFPR
**Projeto Final – 2026/2**

## Autor
- Jad Martins de Lima

## Descrição da abordagem
Foi utilizada a **abordagem clássica** (extração de características + classificação) para classificar imagens de grãos de café em 4 classes de torra: **Dark, Green, Light e Medium**.

**Extração de características – GLCM (Gray-Level Co-occurrence Matrix)**
Descritor de textura diferente dos apresentados em aula (HOG, LBP e histograma de cor). Etapas:
1. Imagens lidas em escala de cinza e redimensionadas para 224x224.
2. Quantização dos níveis de cinza de 256 para 64.
3. Cálculo da GLCM com 3 distâncias (1, 3 e 5 pixels) e 4 ângulos (0°, 45°, 90° e 135°).
4. Extração de 6 propriedades de Haralick por matriz: contrast, dissimilarity, homogeneity, energy, correlation e ASM.
5. Resultado: vetor de **72 características por imagem** (3 × 4 × 6).

**Pré-processamento e classificação**
- Divisão treino/teste: foi utilizada a divisão original do dataset (pastas `train` e `test`).
- Normalização com `StandardScaler` (ajustado apenas nos dados de treino).
- Classificadores comparados: **SVM (kernel RBF)**, **Random Forest** e **KNN (k=5)**.
- Ajuste de hiperparâmetros do SVM (C e gamma) com `GridSearchCV` e validação cruzada de 5 folds, usando apenas o conjunto de treino.

**Métricas:** matriz de confusão, precisão, recall, F1-score e acurácia.

**Ambiente e bibliotecas:** Google Colab, Python, OpenCV, NumPy, Matplotlib, scikit-image, scikit-learn e tqdm.

## Links
- **Repositório com o código (sem o dataset) e o vídeo de apresentação:** [Repositório Github](https://github.com/Jadmartins936/projeto-AS65F)
- **Vídeo de apresentação:** [Vídeo](https://drive.google.com/file/d/1vAaJWcMaGvu_r2L1funFoh_k74bWHPnr/view?usp=sharing)
- **Dataset utilizado (Coffee Bean Dataset, 224x224):** https://www.kaggle.com/datasets/gpiosenka/coffee-bean-dataset-resized-224-x-224

## Resultados (conjunto de teste)
| Classificador | Acurácia |
|---|---|
| SVM (RBF) | 93,75% |
| Random Forest | 100,00% |
| KNN (k=5) | 83,50% |
| SVM otimizado (GridSearchCV) | 93,00% |

**Melhor modelo:** Random Forest, com acurácia de **100,00%** no conjunto de teste (400 imagens, 100 por classe). Precisão, recall e F1-score foram 1,00 em todas as classes e a matriz de confusão não apresentou nenhum erro.

Precisão, recall, F1-score por classe e matriz de confusão: ver o notebook `Projeto_Final_GLCM.ipynb` (seção 9).

## Instruções de uso
1. Baixe o dataset pelo link acima e envie a pasta para o seu Google Drive. Ela deve conter `train/` e `test/`, cada uma com as subpastas `Dark`, `Green`, `Light` e `Medium`.
2. Abra o arquivo `Projeto_Final_GLCM.ipynb` no Google Colab.
3. Na seção "Configuração do dataset", ajuste a variável `HOLDOUT_DIR` para o caminho da pasta no seu Drive (ex.: `/content/drive/MyDrive/archive`).
4. Execute todas as células: *Ambiente de execução → Executar tudo*. Não é necessário GPU.
