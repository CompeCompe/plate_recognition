### Цель проекта:
Данный проект учебный, необходимо создать и обучить модель для распознавания номера и типа машины в видеопотоке, полученном с видеокамеры на КПП

### Результат:
<p align="center"><img src="./helpers/cars-2.gif"\></p>

### Шаги реализации:
1) Датасет содержит три класса(легковая машина, номер, грузовая машина), собрали его из трех частей: 
* скриншоты с камер видеонаблюдения
* скаченные картинки с интернета, для обогащения класса **грузовая машина**
* скаченный готовый датасет из [kaggle](https://www.kaggle.com/datasets/andrewmvd/car-plate-detection)

Произвели разметку классов для Yolo моделей при помощи labelImg.

<a href="https://drive.google.com/uc?export=view&id=1LCW7MpU_oEI_DcCchluVNyIedY8OWVMr"><img src="https://drive.google.com/uc?export=view&id=1LCW7MpU_oEI_DcCchluVNyIedY8OWVMr" style="width: 500px; max-width: 100%; height: auto" title="Click for the larger version." /></a>

2) Обучили на собранном [датасете](https://www.kaggle.com/datasets/kirillpribludenko/number-plates-50-russain-50-others) две модели [Yolov5m](yolov5m.ipynb) и [Yolov7](ALPR.ipynb). 

Лучшие веса для данных моделей:
[Yolo5m](https://drive.google.com/file/d/1htNcnFONfzpevnFL5iw3OpycEK3tG71m/view?usp=sharing)
[Yolo7](https://drive.google.com/file/d/1e5QTOn7kLk5ekQHyR8343c90Hhw3FAEy/view?usp=sharing)

Произвели сравнение по метрикам результатов детекций, чтобы выяснить какая из моделей лучше подходит для данной задачи

**Метрики качества валидационного набора для Yolo7:**
<p align="left"><img src="./helpers/yolo7_val.png"\></p>

**Метрики качества валидационного набора для Yolo5:**
<p align="left"><img src="./helpers/yolov5m_val.png"\></p>

**Метрики скорости тестового набора для Yolo7:**
<p align="left"><img src="./helpers/yolo7_test_s.png"\></p>

**Метрики скорости тестового набора для Yolo5:**
<p align="left"><img src="./helpers/yolov5m_test.png"\></p>

3) В код модели добавили автоматическое распознавание текста при детекции номера, реализованное через easyocr
