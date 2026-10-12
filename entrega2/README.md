# FarmTech Solutions — Comparação de abordagens de visão computacional

Projeto acadêmico da FIAP — PBL Fase 6, Entrega 2.

Equipe 7

## 👨‍🎓 Integrantes

* <a href="#">Luiz Henrique Martins Dias</a>
* <a href="#">Ricardo Colpani Sprocati de Oliveira</a>
* <a href="#">Walter Corradini Ferreira</a>
* <a href="#">Fahd Ozelame Al Khaldi</a>
* <a href="#">André Rohregger Machado</a>

## 👩‍🏫 Professores

### Tutor(a)

* <a href="#">Nicolly Candida Rodrigues de Souza</a>

### Coordenador(a)

* <a href="#">Andre Godoi Chiovato</a>

---

## Apresentação

Esta entrega compara três abordagens de visão computacional, todas aplicadas à base de tomates e cenouras da [Entrega 1](../entrega1/README.md):

| Abordagem | Descrição |
| --- | --- |
| **A. YOLO customizada** | YOLOv5s ajustado na Entrega 1 (`best.pt`, 60 épocas) |
| **B. YOLO tradicional** | YOLOv5s com os pesos padrão do COCO (80 classes), usado sem novo treino |
| **C. CNN do zero** | Rede convolucional própria em Keras, com pesos iniciais aleatórios |

A comparação considera facilidade de uso e integração, precisão, tempo de treinamento ou customização e tempo de inferência. O notebook reúne o código comentado e executado, as saídas, as imagens processadas e a análise crítica dos resultados.

## Acesso à solução

- [Notebook executado — `Equipe7_pbl_fase6.ipynb`](Equipe7_pbl_fase6.ipynb)
- [![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/fiapequipe7/FarmTech_Fase6/blob/main/entrega2/Equipe7_pbl_fase6.ipynb)

## Como executar

1. Abra o notebook no Colab pelo botão acima e selecione **Ambiente de execução → Alterar o tipo de ambiente de execução → GPU T4**.
2. Deixe a pasta `FarmTech_Fase6` da Entrega 1 em `Meu Drive`, seguindo as instruções do [README da Entrega 1](../entrega1/README.md). O notebook usa `dataset/` e `resultados/treino_60_epocas/weights/best.pt`.
3. Execute **Ambiente de execução → Executar tudo** e autorize o acesso ao Google Drive.

O notebook instala o YOLOv5 na mesma versão da Entrega 1 (commit `f9578796`) e baixa os pesos do COCO automaticamente. Figuras, tabelas e o modelo da CNN são salvos em `resultados/entrega2/`, no Drive.

## Resultado resumido

Resultados nas 8 imagens de teste (4 tomates e 4 cenouras), com execução no Google Colab (GPU T4):

| Abordagem | Acurácia no teste | Treino / customização | Inferência GPU | Inferência CPU |
| --- | ---: | --- | ---: | ---: |
| A. YOLO customizada (limiar 0,25) | 50% (4/8) | 74,3 min (Entrega 1) | 11,6 ms | 418,9 ms |
| A. YOLO customizada (limiar 0,10, calibrado na validação) | 100% (8/8) | — | — | — |
| B. YOLO tradicional (mapeamento de classes aprendido no treino) | 75% (6/8) | sem treino; 1,1 s de mapeamento | 11,8 ms | 222,2 ms |
| C. CNN do zero | 87,5% (7/8) nas 5 sementes testadas | 26,6 s | 15,8 ms | 23,7 ms |

- **A. YOLO customizada:** acertou todos os tomates, mas, com o limiar de 0,25 herdado da Entrega 1, não detectou nenhuma cenoura. Com o limiar escolhido na validação, acertou as 8 imagens. A baixa confiança nas cenouras se explica pela rotulação, que tem uma única caixa por foto mesmo quando há maços.
- **B. YOLO tradicional:** reconheceu as cenouras sem nenhum treino, mas não conhece tomates, que o COCO não tem. Os tomates só foram aceitos depois de mapear `apple` e `orange` para tomate.
- **C. CNN do zero:** é a mais leve (0,24 milhão de parâmetros), treina em segundos e é a mais rápida em CPU, mas apenas classifica a imagem: não localiza nem conta objetos.

Com 8 imagens de teste, os intervalos de confiança são largos, e as diferenças de acurácia não são estatisticamente conclusivas.

As análises detalhadas, as limitações e as imagens processadas estão no notebook.

## Tecnologias

Google Colab (GPU T4), PyTorch, YOLOv5, Keras 3 (backend PyTorch), scikit-learn, pandas e Matplotlib.

## Referências

- [YOLOv5 — repositório oficial](https://github.com/ultralytics/yolov5)
- [COCO — Common Objects in Context](https://cocodataset.org/)
- [Keras 3 — documentação](https://keras.io/)
- [Grad-CAM — Selvaraju et al., 2017](https://arxiv.org/abs/1610.02391)
