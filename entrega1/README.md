# FarmTech Solutions — Detecção de tomates e cenouras

Projeto acadêmico da FIAP — PBL Fase 6, Entrega 1.

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

Este projeto explora a detecção de tomates e cenouras em imagens com o YOLOv5s. Foram realizados dois treinamentos, com 30 e 60 épocas, para comparar as métricas de validação e avaliar o modelo selecionado em imagens de teste.

O relatório completo, os códigos comentados, as saídas executadas, os gráficos e as imagens de teste processadas estão no notebook do Google Colab.

## Acesso à solução

- [Notebook e relatório completo no Google Colab](https://drive.google.com/drive/folders/1fji14pxnjaO4rJPIXNukBUqzkdZygwz1?usp=drive_link)
- [Vídeo demonstrativo no YouTube — não listado, até 5 minutos](INSERIR_LINK_VIDEO)

## Dataset e ferramentas

O dataset contém 80 imagens, divididas conforme o enunciado:

| Conjunto | Tomates | Cenouras | Total |
| --- | ---: | ---: | ---: |
| Treino | 32 | 32 | 64 |
| Validação | 4 | 4 | 8 |
| Teste | 4 | 4 | 8 |
| **Total** | **40** | **40** | **80** |

As imagens foram rotuladas no Make Sense IA com polígonos e exportadas em COCO JSON. No notebook, as marcações foram convertidas em retângulos no formato YOLO para detecção de objetos.

Foram utilizados Google Drive, Google Colab, Make Sense IA, YOLOv5s e PyTorch.

## Como executar

1. Abra o notebook pelo link acima e salve uma cópia no seu Google Drive.
2. Acesse o dataset compartilhado e copie ou baixe seu conteúdo para uma pasta chamada `dataset` dentro de `Meu Drive/FarmTech_Fase6`, preservando as subpastas e os arquivos.
3. Configure o ambiente do Colab para utilizar GPU.
4. Confira a variável `project_path`: ela deve apontar para `/content/drive/MyDrive/FarmTech_Fase6`. Ajuste-a se utilizar outro local.
5. Execute as células na ordem apresentada, começando pela conexão com o Drive, e autorize o acesso à sua conta.

O acesso ao notebook não monta automaticamente o Drive do autor. Para reproduzir as execuções, os dados precisam estar disponíveis no Drive de quem executar.

Os treinamentos geram os modelos utilizados nas avaliações posteriores. Algumas células dependem de variáveis criadas anteriormente; após reiniciar o ambiente, execute novamente as etapas necessárias na ordem.

## Resultado resumido

O modelo de 60 épocas foi selecionado pelo maior mAP@0.5:0.95 na validação: **36,7%**, contra **19,5%** do modelo de 30 épocas.

No teste, o modelo escolhido apresentou mAP@0.5 de **59,3%** e mAP@0.5:0.95 de **30,2%**. Na visualização com confiança mínima de 25%, os quatro tomates receberam detecções e as quatro cenouras não.

O resultado evidencia desempenho desigual entre as classes. O pequeno dataset e o teste com apenas quatro imagens por classe limitam as conclusões. As análises detalhadas e os exemplos visuais estão no notebook.

## Referências

- [YOLOv5 — repositório oficial](https://github.com/ultralytics/yolov5)
- [Make Sense IA](https://www.makesense.ai/)
- [Google Colab](https://colab.research.google.com/)

