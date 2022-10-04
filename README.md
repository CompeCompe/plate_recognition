### Цель проекта:
Данный проект учебный, необходимо создать и обучить модель для распознавания номера и типа машины в видеопотоке, полученного с видеокамеры на КПП

### Результат:
*тут должна быть гифка видоса*

### Шаги реализации:
1) Датасет содержит три класса(легковая машина, номер, грузовая машина), собрали его из трех частей: 
* скриншоты с камер ведионаблюдения
* скаченные картинки с интернета, для обогащения класса **грузовая машина**
* скачаенный готовый датасет из [kaggle](https://www.kaggle.com/datasets/andrewmvd/car-plate-detection)
Произвели разметку классов для Yolo моделей при помощи labelImg.

![Pic](https://drive.google.com/uc?export=view&id=1LCW7MpU_oEI_DcCchluVNyIedY8OWVMr)

<a href="https://drive.google.com/uc?export=view&id=1LCW7MpU_oEI_DcCchluVNyIedY8OWVMr"><img src="https://drive.google.com/uc?export=view&id=1LCW7MpU_oEI_DcCchluVNyIedY8OWVMr" style="width: 500px; max-width: 100%; height: auto" title="Click for the larger version." /></a>

2) Обучили на собранном датасете две модели Yolov5 и Yolov7. Произвели сравнение по метрикам результата детекции, чтобы выяснить как из моделей лучше подходит для этой задачи
4) В код модели добавили автоматическое распознавание текста при детекции номера, реализованное через easyocr
5) Результат: 
