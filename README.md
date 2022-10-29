### Цель проекта:
Данный проект учебный, необходимо создать и обучить модель для распознавания номера и типа машины в видеопотоке, полученном с видеокамеры на КПП.

**ПРИМЕЧАНИЕ:**Все расчеты, а также измериния метрик и скорости производились в **Google Colab на GPU Tesla T4 16Gb**, так как хороших собственных мощностей для таких трудоемких расчетов не имеем.

### Результат:
<p align="center"><img src="./helpers/cars-2.gif"\></p>

### Шаги реализации:
1) Датасет содержит три класса(легковая машина, номер, грузовая машина), собрали его из трех частей: 
* скриншоты с камер видеонаблюдения
* скаченные картинки с интернета, для обогащения класса **грузовая машина**
* скаченный готовый датасет из [kaggle](https://www.kaggle.com/datasets/andrewmvd/car-plate-detection)

Произвели разметку классов для Yolo моделей при помощи labelImg.

<a href="https://drive.google.com/uc?export=view&id=1LCW7MpU_oEI_DcCchluVNyIedY8OWVMr"><img src="https://drive.google.com/uc?export=view&id=1LCW7MpU_oEI_DcCchluVNyIedY8OWVMr" style="width: 500px; max-width: 100%; height: auto" title="Click for the larger version." /></a>

<a href="./helpers/labelimg.png"><img src="./helpers/labelimg.png" style="width: 500px; max-width: 100%; height: auto" title="Click for the larger version." /></a>

2) Обучили на собранном [датасете](https://www.kaggle.com/datasets/kirillpribludenko/number-plates-50-russain-50-others) две модели [Yolov5m](yolov5m.ipynb) и [Yolov7](ALPR.ipynb). 

Лучшие веса для данных моделей:
[Yolov5m](https://drive.google.com/file/d/1htNcnFONfzpevnFL5iw3OpycEK3tG71m/view?usp=sharing)
[Yolov7](https://drive.google.com/file/d/1e5QTOn7kLk5ekQHyR8343c90Hhw3FAEy/view?usp=sharing)

3) В код модели добавили автоматическое распознавание текста при детекции номера, реализованное через easyocr

4) Сравнение моделей

В качестве метрики была выбрана популяная mAP для детекции, тем более, что ее расчет вшит в модели yolo. Произвели сравнение по данной метрике, чтобы понять какая модель лучше подходит под нашу задачу.

**Метрики качества валидационного набора для Yolov7:**
<p align="left"><img src="./helpers/yolo7_val.png"\></p>

**Метрики качества валидационного набора для Yolov5m:**
<p align="left"><img src="./helpers/yolov5m_val1.png"\></p>

Как видно из табличных данных по столбцу mAP@.5:.95 Yolo7 чуть лучше распознает класс грузовиков в остальных классах примерно одинаково. Поэтому проведем дополнительно замеры по скорости детекции и скорости общего решения, для окончательного выбора модели для нашей задачи.

**Метрики скорости детекции тестового набора для Yolov7 (дополнительно был поставлен флаг --v5-metric):**
<p align="left"><img src="./helpers/yolo7_test_s.png"\></p>

**Метрики скорости детекции тестового набора для Yolov5m:**
<p align="left"><img src="./helpers/yolov5m_test.png"\></p>

**Метрики общей скорости тестового набора для Yolov7 (дополнительно был поставлен флаг --v5-metric):**
<p align="left"><img src="./helpers/yolo7_test_total.png"\></p>

**Метрики общей скорости тестового набора для Yolov5m:**
<p align="left"><img src="./helpers/yolov5m_test_total.png"\></p>

На основани полученных результатов была выбрана модель **Yolov5**, так как ее скорость детекции практически в два раза быстрее, при сравнительно одинаковом качесте обнаружения.