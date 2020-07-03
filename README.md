
<a href="https://apps.apple.com/app/id1452689527" target="_blank">
<img src="https://user-images.githubusercontent.com/26833433/82944393-f7644d80-9f4f-11ea-8b87-1a5b04f555f1.jpg" width="1000"></a>
&nbsp

Este reposit�rio � uma releitura do original, que pode ser encontrado no link: [https://github.com/ultralytics/yolov5](https://github.com/ultralytics/yolov5) . 

Que fique claro a essa implementa��o do Yolo, considerada o YoloV5, n�o � oficial da Darknet, mas foi desenvolvimento pela Ultralytics em Pytorch.

Aqui vamos tentar ser mais pr�ticos, mas toda a teoria e os benchmarks, podem ser consultados no link acima.

**Atualmente este reposit�rio est� em frequente desenvolvimento e portanto, � poss�vel que existam descontinua��es ou modifica��es frequentes na api.**

<img src="https://user-images.githubusercontent.com/26833433/85340570-30360a80-b49b-11ea-87cf-bdf33d53ae15.png" width="1000">


## Modelos Pr�-treinados

| Modelo | AP<sup>val</sup> | AP<sup>test</sup> | AP<sub>50</sub> | Speed<sub>GPU</sub> | FPS<sub>GPU</sub> || params | FLOPS |
|---------- |------ |------ |------ | -------- | ------| ------ |------  |  :------: |
| [YOLOv5s](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)    | 36.6     | 36.6     | 55.8     | **2.1ms** | **476** || 7.5M   | 13.2B
| [YOLOv5m](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)    | 43.4     | 43.4     | 62.4     | 3.0ms     | 333     || 21.8M  | 39.4B
| [YOLOv5l](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)    | 46.6     | 46.7     | 65.4     | 3.9ms     | 256     || 47.8M  | 88.1B
| [YOLOv5x](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)    | **48.4** | **48.4** | **66.9** | 6.1ms     | 164     || 89.0M  | 166.4B
| [YOLOv3-SPP](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J)  | 45.6     | 45.5     | 65.2     | 4.5ms     | 222     || 63.0M  | 118.0B



## Requerimentos

* Python 3.7 ou superior. Todas as depend�ncias necess�rias est�o no`requirements.txt`, incluindo o `torch >= 1.5`. 

## Instala��o
**1-** Clone este reposit�rio:

    $ git clone https://github.com/eduardodutragoncalves/Yolov5Ultralytics.git

**2-** Entre no diret�rio 

    $ cd Yolov5Ultralytics

**3-** execute:  
```bash
$ pip install -U -r requirements.txt
```
## Infer�ncia(Teste)

Quando voc� executar o comando para infer�ncia, o script far� o download e executar� essa infer�ncia no [Modelo Pr�-treinado](https://drive.google.com/open?id=1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J), que voc� especificou.
*Caso n�o ocorra o download, pode ser por mudan�as eventuais no path do gDrive. Voc� pode fazer o download manualmente e adicion�-lo no diret�rio `models`*.

O resultado da sua infer�ncia, podem ser consultados no diret�rio `.inference/output`.

**Par�metros**
**weights**  - Informe qual ser� o modelo/pesos que voc� deseja usar na sua infer�ncia (yolov5x.pt,yolov5m.pt,yolov5l.pt,yolov5s.pt)
**img**  - Refere-se ao tamanho da imagem convertida no momento do treinamento. Mudar esse par�metros pode acarretar em quedas da acur�cia da sua infer�ncia.
**conf** - Refere-se a *Confidence*, que no caso � de 0.4(40%). Quanto maior o valor, maior acuracidade voc� estar� exigindo da infer�ncia.
**source** - Refere-se ao tipo de midia:
      Imagem:  ('.bmp' , '.jpg' , '.jpeg' , '.png', '.tif' , '.dng')
      v�deo: ('.mov', '.avi', '.mp4', '.mpg', '.mpeg', '.m4v', '.wmv', '.mkv')
      diret�rios: ('/dir')
      streams: ('rtsp', 'http')
**output** - Refere-se ao nome da m�dia na sa�da, ap�s a infer�ncia. Caso n�o informe, o algoritmo vai gerar um arquivo de resultado, com o mesmo nome e extens�o do arquivo original(source)

* Inferindo uma imagem  
```bash
$ python detect.py --weights yolov5l.pt --img 416 --conf 0.4 --source ./inference/images/file1.jpg
```
* Inferindo um v�deo 
No caso do v�deo, fiz um pequeno experimento, para mostrar na pr�tica as diferen�as de velocidade e acuracidade, para os modelos pr�-treinados. Estes modelos, usaram o dataset [test-dev2017](http://cocodataset.org/#upload), muito comum para gera��o de modelos e benchmarks. Ele possui atualmente 80 classes na infer�ncia.

[Benchmark dos modelos default](https://youtu.be/amSsMBO75I8)
```bash
$ python detect.py --weights yolov5x.pt --img 416 --conf 0.4 --source ./inference/videos/YoloV5.mp4
```
*Altere o weights para voc� executar a infer�ncia com v�rios n�veis de velocidade e acur�cia, para avaliar qual � o mais adequado � sua necessidade. Para visualizar as diferen�as, clique no link acima*.

* Inferindo em um diret�rio  
Quando voc� precisa processar lotes de imagens e v�deos, por exemplo para coleta dos resultados depois, voc� pode colocar todas as m�dias em determinado diret�rio que ele vai executar a infer�ncia para tipo tipo de m�dia e extens�o, dentro daquele diret�rio.
```bash
$ python detect.py --weights yolov5l.pt --img 416 --conf 0.4 --source ./inference/images/
```
* Inferindo na WebCam  
No caso de rodar a infer�ncia pela webcam, nos casos em que voc� tiver mais de 1 webcam no seu PC/note e quiser direcionar, o --source 0 indica que o algoritmo vai capturar a primeira webcam no stack do SO. Caso queira mudar, basta variar o 0, at� encontrar o �ndice da c�mera desejada.
```bash
$ python detect.py --weights yolov5l.pt --img 416 --conf 0.4 --source 0
```
* Inferindo Stream
Aponte o --source pra um stream quando voc� quer capturar um v�deo que estiver sendo transmitido naquele momento. Voc� pode baixar um aplicativo de stream de v�deo, como o IPWebCam. Start o v�deo dele e passa o ip:porta para que a infer�ncia aconte�a.
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


## Cita��es

[Post original](https://github.com/ultralytics/yolov5)


