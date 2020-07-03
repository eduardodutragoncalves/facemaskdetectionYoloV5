
<a href="https://apps.apple.com/app/id1452689527" target="_blank">
<img src="https://user-images.githubusercontent.com/26833433/82944393-f7644d80-9f4f-11ea-8b87-1a5b04f555f1.jpg" width="1000"></a>
&nbsp

Este repositório é uma releitura do original, que pode ser encontrado no link: [https://github.com/ultralytics/yolov5](https://github.com/ultralytics/yolov5) . 

Que fique claro a essa implementação do Yolo, considerada o YoloV5, não é oficial da Darknet, mas foi desenvolvimento pela Ultralytics em Pytorch.

Aqui vamos tentar ser mais práticos, mas toda a teoria e os benchmarks, podem ser consultados no link acima.

**Atualmente este repositório está em frequente desenvolvimento e portanto, é possível que existam descontinuações ou modificações frequentes na api.**

<img src="https://user-images.githubusercontent.com/26833433/85340570-30360a80-b49b-11ea-87cf-bdf33d53ae15.png" width="1000">


## Modelos Pré-treinados

| Modelo | AP<sup>val</sup> | AP<sup>test</sup> | AP<sub>50</sub> | Speed<sub>GPU</sub> | FPS<sub>GPU</sub> || params | FLOPS |
|---------- |------ |------ |------ | -------- | ------| ------ |------  |  :------: |
| [YOLOv5s](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)    | 36.6     | 36.6     | 55.8     | **2.1ms** | **476** || 7.5M   | 13.2B
| [YOLOv5m](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)    | 43.4     | 43.4     | 62.4     | 3.0ms     | 333     || 21.8M  | 39.4B
| [YOLOv5l](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)    | 46.6     | 46.7     | 65.4     | 3.9ms     | 256     || 47.8M  | 88.1B
| [YOLOv5x](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)    | **48.4** | **48.4** | **66.9** | 6.1ms     | 164     || 89.0M  | 166.4B
| [YOLOv3-SPP](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)  | 45.6     | 45.5     | 65.2     | 4.5ms     | 222     || 63.0M  | 118.0B



## Requerimentos

* Python 3.7 ou superior. Todas as dependências necessárias estão no`requirements.txt`, incluindo o `torch >= 1.5`. 

## Instalação
**1-** Clone este repositório:

    $ git clone https://github.com/eduardodutragoncalves/Yolov5Ultralytics.git

**2-** Entre no diretório 

    $ cd Yolov5Ultralytics

**3-** execute:  
```bash
$ pip install -U -r requirements.txt
```
## Inferência(Teste)

Quando você executar o comando para inferência, o script fará o download e executará essa inferência no [Modelo Pré-treinado](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J), que você especificou.
*Caso não ocorra o download, pode ser por mudanças eventuais no path do gDrive. Você pode fazer o download manualmente e adicioná-lo no diretório `models`*.

O resultado da sua inferência, podem ser consultados no diretório `.inference/output`.

**Parâmetros**
**weights**  - Informe qual será o modelo/pesos que você deseja usar na sua inferência (yolov5x.pt,yolov5m.pt,yolov5l.pt,yolov5s.pt)
**img**  - Refere-se ao tamanho da imagem convertida no momento do treinamento. Mudar esse parâmetros pode acarretar em quedas da acurácia da sua inferência.
**conf** - Refere-se a *Confidence*, que no caso é de 0.4(40%). Quanto maior o valor, maior acuracidade você estará exigindo da inferência.
**source** - Refere-se ao tipo de midia:
      Imagem:  ('.bmp' , '.jpg' , '.jpeg' , '.png', '.tif' , '.dng')
      vídeo: ('.mov', '.avi', '.mp4', '.mpg', '.mpeg', '.m4v', '.wmv', '.mkv')
      diretórios: ('/dir')
      streams: ('rtsp', 'http')
**output** - Refere-se ao nome da mídia na saída, após a inferência. Caso não informe, o algoritmo vai gerar um arquivo de resultado, com o mesmo nome e extensão do arquivo original(source)

* Inferindo uma imagem  
```bash
$ python detect.py --weights yolov5l.pt --img 416 --conf 0.4 --source ./inference/images/file1.jpg
```
* Inferindo um vídeo 
No caso do vídeo, fiz um pequeno experimento, para mostrar na prática as diferenças de velocidade e acuracidade, para os modelos pré-treinados. Estes modelos, usaram o dataset [test-dev2017](http://cocodataset.org/#upload), muito comum para geração de modelos e benchmarks. Ele possui atualmente 80 classes na inferência.

[Benchmark dos modelos default](https://youtu.be/amSsMBO75I8)
```bash
$ python detect.py --weights yolov5x.pt --img 416 --conf 0.4 --source ./inference/videos/YoloV5.mp4
```
*Altere o weights para você executar a inferência com vários níveis de velocidade e acurácia, para avaliar qual é o mais adequado à sua necessidade. Para visualizar as diferenças, clique no link acima*.

* Inferindo em um diretório  
Quando você precisa processar lotes de imagens e vídeos, por exemplo para coleta dos resultados depois, você pode colocar todas as mídias em determinado diretório que ele vai executar a inferência para tipo tipo de mídia e extensão, dentro daquele diretório.
```bash
$ python detect.py --weights yolov5l.pt --img 416 --conf 0.4 --source ./inference/images/
```
* Inferindo na WebCam  
No caso de rodar a inferência pela webcam, nos casos em que você tiver mais de 1 webcam no seu PC/note e quiser direcionar, o --source 0 indica que o algoritmo vai capturar a primeira webcam no stack do SO. Caso queira mudar, basta variar o 0, até encontrar o índice da câmera desejada.
```bash
$ python detect.py --weights yolov5l.pt --img 416 --conf 0.4 --source 0
```
* Inferindo Stream
Aponte o --source pra um stream quando você quer capturar um vídeo que estiver sendo transmitido naquele momento. Você pode baixar um aplicativo de stream de vídeo, como o IPWebCam. Start o vídeo dele e passa o ip:porta para que a inferência aconteça.
```bash
$ python detect.py --weights yolov5l.pt --img 416 --conf 0.4 --source rtsp://170.93.143.139/rtplive/470011e600ef003a004ee33696235daa
```
```bash
$ python detect.py --weights yolov5l.pt --img 416 --conf 0.4 --source ```
http://112.50.243.8/PLTV/88888888/224/3221225900/1.m3u8
```

## Tutoriais

* [Notebook](https://github.com/ultralytics/yolov5/blob/master/tutorial.ipynb) <a href="https://colab.research.google.com/github/ultralytics/yolov5/blob/master/tutorial.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a>
* [Train Custom Data](https://github.com/ultralytics/yolov5/wiki/Train-Custom-Data)
* [Google Cloud Quickstart Guide](https://github.com/ultralytics/yolov5/wiki/GCP-Quickstart)
* [Docker Quickstart Guide](https://github.com/ultralytics/yolov5/wiki/Docker-Quickstart) ![Docker Pulls](https://img.shields.io/docker/pulls/ultralytics/yolov5?logo=docker)


## Citações

[Post original](https://github.com/ultralytics/yolov5)


