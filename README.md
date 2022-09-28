# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Мосин Дмитрий Сергеевич
- РИ210936
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
### Написать программы Hello World на Python и Unity. 
Ход работы:
- Для Python в отчете привести скриншоты с демонстрацией сохранения документа google.colab на свой диск с запуском программы, выводящей сообщение Hello World.
Скриншот запуска кода print('Hello, World') на Python в Google.colab:

![image](https://user-images.githubusercontent.com/112868100/192851723-67302cc3-6474-4b05-be13-576eb9a9b5b5.png)

Скриншот сохранения блокнота (кода) на Google.Disk:

![image](https://user-images.githubusercontent.com/112868100/192852402-1c4f1d82-d9dd-451f-bba9-26ed81917840.png)

-Для Unity  в отчете привести скришноты вывода сообщения Hello World в консоль.

Скриншот кода print('Hello, World') на Unity:

![image](https://user-images.githubusercontent.com/112868100/192853120-122a75d4-056d-492f-8963-bf08264da99f.png)

Для выполнения скрипта, недостаточно запуска самого проекта, необходимо привязать скрипт к какому-либо объекту:

Скриншот вывода 'Hello,World' в консоль: 

![image](https://user-images.githubusercontent.com/112868100/192853594-8d55897c-4934-4174-a7d6-84f04e24cb37.png)


## Задание 2
### В разделе «ход работы» пошагово выполнить каждый пункт с описанием и примером реализации задачи по теме лабораторной работы.

Ход работы
- 1)	Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

Код на Python в Google.Collab. Мы задаем случайные наборы данных и приводим их к массиву:

![image](https://user-images.githubusercontent.com/112868100/192855218-f037082e-c7ba-463d-8da3-ab6747609883.png)

Но для начала необходимо установить необходимые библиотеки matplotlib для отрисовки и numpy для вычислений. 

![image](https://user-images.githubusercontent.com/112868100/192855027-b50a6de9-32d2-4fb5-a67b-01c9f68e1740.png)

Затем мы отрисовываем наши данные на графике:

![image](https://user-images.githubusercontent.com/112868100/192855936-492396ff-7f56-4302-aa45-3a9a9e8aea05.png)

- 2)	Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. 
```py
def model(a, b, x):
  return a*x + b
```

Функция потерь: функция потерь среднеквадратичной ошибки. 
```py
def loss_function(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  return (0.5 / num) * (np.square(prediction - y)).sum()
```

Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.
```py
def optimize(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  #Обновление значений a и b, поиском частных производных функций потерь на a и b
  da = (1.0 / num) * ((prediction - y) * x).sum()
  db = (1.0 / num) * ((prediction - y).sum())
  a = a - Lr * da
  b = b - Lr * db
  return a, b
```

Функция итерации: возвращает значения a и b.
```py
def iterate(a, b, x, y, times):
  for i in range(times):
    a, b= optimize(a, b, x, y)
  return a, b
```

- 3)	Начать итерацию.
Шаг 1. Инициализация и модель итеративной оптимизации
```py
a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001

a, b = iterate(a, b, x, y, 1)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)
```

Скриншот первой итерации:

![image](https://user-images.githubusercontent.com/112868100/192857601-0d3d4693-eda7-4e5a-b722-ef43cb15e37c.png)

Шаг 2. На второй итерации отображаются значения параметров, значения потерь и эффекты визуализации после итерации.
```py
a, b = iterate(a, b, x, y, 2)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)
```

Скриншот второй итерации:

![image](https://user-images.githubusercontent.com/112868100/192857972-46f42a09-2fa4-4adf-ab17-27ac955aca92.png)


Шаг 3. Третья итерация показывает значения параметров, значения потерь и эффекты визуализации после итерации.
```py
a, b = iterate(a, b, x, y, 3)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)
```

Скриншот третьей итерации:

![image](https://user-images.githubusercontent.com/112868100/192858180-06c8ab54-990d-4989-ac37-b4e11c593898.png)

Шаг 4. На четвертой итерации отображаются значения параметров, значения потерь и эффекты визуализации после итерации.
```py
a, b = iterate(a, b, x, y, 4)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)
```

Скриншот четвертой итерации:

![image](https://user-images.githubusercontent.com/112868100/192858343-b40ed9d4-f921-4e1a-8c1a-3202bf55e021.png)

Шаг 5. Пятая итерация показывает значения параметров, значения потерь и эффекты визуализации после итерации.
```py
a, b = iterate(a, b, x, y, 5)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)
```

Скриншот пятой итерации:

![image](https://user-images.githubusercontent.com/112868100/192858518-f144dba7-589b-4e40-8d09-c9d295df6028.png)

Шаг 6. 10000-я итерация, показывающая значения параметров, значения потерь и эффекты визуализации после итерации.
```py
a, b = iterate(a, b, x, y, 10000)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)
```

Скриншот шестой итерации:

![image](https://user-images.githubusercontent.com/112868100/192858871-0ed9d245-b37d-4994-aeb1-4db752b0fcf7.png)

Анализируя изменения значений в консоли и изменение графиков по итерациям, можно сделать вывод о том, что значения аргументов a и b увеличиваются прямопропорционально увеличению количества итерации, а вот значения потерь, наоборот, уменьшаются.


## Задание 3
### Изучить код на Python и ответить на вопросы:

Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.


## Выводы

В ходе лабораторной работы, я познакомился с основными операторами в Python на примере реализции линейной регресии. При выполнении задач, мною были изучены: оператор вывода данных на консоль в Python и Unity, библиотеки matplotlib и numpy дли вычисления и вывода графиков на экран, различные методы, содержащиеся в данных библиотеках. В ходе выполнения второго задания были выявлены закономерности увеличения значений аргументов a и b с увеличением итерации линейной регрессии, и наоборот уменьшением потерь с увеличением итераций. 

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
