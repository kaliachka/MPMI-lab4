Лабораторная работа 4
===
Использование техник аугментации данных для улучшения сходимости процесса обучения нейронной сети на примере решения задачи классификации Oregon Wildlife
---
### 1. С использованием, техники обучения Transfer Learning и оптимальной политики изменения темпа обучения обучить нейронную сеть EfficientNet-B0 (предварительно обученную на базе изображений imagenet) для решения задачи классификации изображений Oregon WildLife с использованием следующих техник аугментации данных:

#### Аугментация данных (англ. data augmentation) — это методика создания дополнительных данных из имеющихся данных.

* 1.1. Манипуляции с яркостью и контрастом:
##### В первом пункт емы использовали технику аугментации изображений путем манипуляции с яркостью и контрастом. Для реализации данного способа были написаны функции:
```
def contrast(image, label):
    return tf.image.adjust_contrast(image, 0.4), label

def brightness(image, label):
    return tf.image.adjust_brightness(image, delta=0.1), label
```
#####  Функция contrast возвращает tf.image.adjust_contrast(image, contrast_factor), где параметр image - входное изображение и contrast_factor - множитель типа float для регулировки контраста. Функция brightness возвращает tf.image.adjust_brightness(image, delta), где параметр image - входное изображение и delta - скалярная величина, добавляемая к значениям пикселей.

##### Функция вызывается в TFRecordDataset:

```
return tf.data.TFRecordDataset(filenames)\
    .map(contrast)\
    .map(brightness)\
```
##### Для нахождения оптимальных значений мною были выбраны следующие параметры:

* contrast_factor = 0.4, delta = 0.1;
* contrast_factor = 0.5, delta = 0.05;
* contrast_factor = 0.5, delta = 0.1;
* contrast_factor = 0.5, delta = 0.2;
* contrast_factor = 1, delta = 1;
* contrast_factor = 3, delta = 0.5;
* contrast_factor = 5, delta = 0.1;

**График метрики точности:**

![2](https://user-images.githubusercontent.com/59210216/112891910-5ac78a80-90e1-11eb-8d88-f346bc7d0fe8.jpg)

![1](https://user-images.githubusercontent.com/59210216/112891891-569b6d00-90e1-11eb-8e33-98bc49e92090.jpg)

**График функции потерь:**

![4](https://user-images.githubusercontent.com/59210216/112891925-61560200-90e1-11eb-8cdc-35633ac32de9.jpg)

![3](https://user-images.githubusercontent.com/59210216/112891917-5e5b1180-90e1-11eb-98ce-dcc23772a265.jpg)

* 1.2.1. Поворот изображения на случайный угол:

![1](https://user-images.githubusercontent.com/59210216/112891940-67e47980-90e1-11eb-833b-698282ae106b.jpg)

![2](https://user-images.githubusercontent.com/59210216/112891958-6c109700-90e1-11eb-95cb-fb90d71b4952.jpg)

![3](https://user-images.githubusercontent.com/59210216/112891971-6f0b8780-90e1-11eb-9a98-ecb10def79d8.jpg)

![4](https://user-images.githubusercontent.com/59210216/112891983-729f0e80-90e1-11eb-9cbc-5528a712b34a.jpg)

* 1.2.2. Поворот изображения на случайный угол с использованием параметра режим заполнения fill_mode:

![1](https://user-images.githubusercontent.com/59210216/112892004-792d8600-90e1-11eb-8478-94fb9a0e0294.jpg)

![2](https://user-images.githubusercontent.com/59210216/112892025-7fbbfd80-90e1-11eb-964b-a1802b1a1794.jpg)

![3](https://user-images.githubusercontent.com/59210216/112892050-8480b180-90e1-11eb-982a-e0acc17f6bf9.jpg)

![4](https://user-images.githubusercontent.com/59210216/112892056-877ba200-90e1-11eb-894b-d37c7644c413.jpg)

* 1.3. Использование случайной части изображения:

![1](https://user-images.githubusercontent.com/59210216/112892077-8e0a1980-90e1-11eb-8d4f-a022a2c38c92.jpg)

![2](https://user-images.githubusercontent.com/59210216/112892099-95312780-90e1-11eb-8057-060d4a0c3f12.jpg)

![3](https://user-images.githubusercontent.com/59210216/112892113-98c4ae80-90e1-11eb-82c5-4267994b0dde.jpg)

![4](https://user-images.githubusercontent.com/59210216/112892122-9bbf9f00-90e1-11eb-8ed6-e0719ca91765.jpg)

* 1.4. Добавление случайного шума:

![1](https://user-images.githubusercontent.com/59210216/112892150-a417da00-90e1-11eb-900f-1d0dbc14ca78.jpg)

![2](https://user-images.githubusercontent.com/59210216/112892160-a712ca80-90e1-11eb-8b7d-315c8e87a5d8.jpg)

![3](https://user-images.githubusercontent.com/59210216/112892166-a9752480-90e1-11eb-98c1-fe7b07921e05.jpg)

![4](https://user-images.githubusercontent.com/59210216/112892177-ab3ee800-90e1-11eb-88f6-ce7421ae168b.jpg)



### 2. Для каждой индивидуальной техники аугментации определить оптимальный набор параметров:

### 3. Обучить нейронную сеть с использованием оптимальных техник аугментации данных 2a-d совместно:
