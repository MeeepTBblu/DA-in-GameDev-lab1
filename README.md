# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Мосин Дмитрий Сергеевич
- РИ210936
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
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
познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Постановка задачи.
В данной лабораторной работе мы создадим ML-агент и будем тренировать нейросеть, задача которой будет заключаться в управлении шаром. Задача шара заключается в том, чтобы оставаясь на плоскости находить кубик, смещающийся в заданном случайном диапазоне координат.

## Задание 1
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity. При выполнении задания можно использовать видео-материалы и исходные данные, предоставленные преподавателями курса.

Ход работы:

--------------------------------------------------------------------------------------------

- Создайте новый пустой 3D проект на Unity.

--------------------------------------------------------------------------------------------

![image](https://user-images.githubusercontent.com/112868100/198266119-9ee84f72-5ca4-4ef0-8b11-b97f89e07fa0.png)

![image](https://user-images.githubusercontent.com/112868100/198266254-022aa263-1bd4-4018-8df6-6d491663979d.png)

--------------------------------------------------------------------------------------------

- Скачайте папку с ML агентом. Вы найдете ее в облаке с исходными файлами к лабораторной работе – ml-agents-release_19.

--------------------------------------------------------------------------------------------

Скачиваем папку по предложенной ссылке

![image](https://user-images.githubusercontent.com/112868100/198266545-50ebda54-c673-4469-af33-40ffe3a82376.png)

--------------------------------------------------------------------------------------------

- В созданный проект добавьте ML Agent, выбрав Window - Package Manager - Add Package from disk. Последовательно добавьте .json – файлы:
    - ml-agents-release_19 / com,unity.ml-agents / package.json
    - ml-agents-release_19 / com,unity.ml-agents.extensions / package.json

--------------------------------------------------------------------------------------------

В проекте переходим в Package Manager 

![image](https://user-images.githubusercontent.com/112868100/198267555-248c7bc1-f041-48ad-b8a5-974334c8870e.png)

--------------------------------------------------------------------------------------------
Переходим в панель добавления файла в проект

![image](https://user-images.githubusercontent.com/112868100/198267694-a218e441-ed9a-43fe-bcd2-19565b9b9c2f.png)

--------------------------------------------------------------------------------------------
Добавляем файл package.json из папки com.unity.ml-agents

![image](https://user-images.githubusercontent.com/112868100/198268294-c55a047b-be5e-49ea-ad31-e5d48f1e43cf.png)

--------------------------------------------------------------------------------------------
Добавляем файл package.json из папки com.unity.ml-agents.extensions

![image](https://user-images.githubusercontent.com/112868100/198269675-e5d3221b-39ce-488f-a8f4-e334bc1d9285.png)

--------------------------------------------------------------------------------------------

- Если все сделано правильно, то во вкладке с компонентами (Components) внутри Unity вы увидите строку ML Agent.

--------------------------------------------------------------------------------------------

Наблюдаем появление соответствующего компонента в Components, значит все сделано правильно

![image](https://user-images.githubusercontent.com/112868100/198269926-43866500-8d9c-4ef1-b77e-c7d8b5d2d3d8.png)

--------------------------------------------------------------------------------------------

- Далее запускаем Anaconda Prompt для возможности запуска команд через консоль.

--------------------------------------------------------------------------------------------

Следующим шагом заупскаем Anaconda Promt от имени администратора

![image](https://user-images.githubusercontent.com/112868100/198273551-ebd457d7-c07d-4deb-81df-edbd2336c05f.png)

--------------------------------------------------------------------------------------------

- Далее пишем серию команд для создания и активации нового ML-агента, а также для скачивания необходимых библиотек:
    - mlagents 0.28.0;
    - torch 1.7.1;

--------------------------------------------------------------------------------------------
    
По предложенным видео-материалам пишем код для установки соотвествующих команд

```py
conda create -n MLAgents python=3.6
conda activate MLAgents
```

![image](https://user-images.githubusercontent.com/112868100/198274394-8d7c3238-4bfa-4a6d-b930-e9f3069e05b7.png)

--------------------------------------------------------------------------------------------

```
pip install mlagents==0.28.0
```

![image](https://user-images.githubusercontent.com/112868100/198274887-ec2db1bd-6988-4f67-a65c-cc3f30af31a5.png)

--------------------------------------------------------------------------------------------

```
pip install torch--1.7.1 -f https://download.pytorch.org/wh1/torch_stable.html
```

![image](https://user-images.githubusercontent.com/112868100/198280272-9bdaf79d-ec84-4f07-8a82-37c2a4c1b368.png)

--------------------------------------------------------------------------------------------

Переключаем MlAgents на дикректорию с проектом

![image](https://user-images.githubusercontent.com/112868100/201081188-d4f3b12d-8b2d-47d0-8e20-d3416fd40d60.png)

--------------------------------------------------------------------------------------------

- Создайте на сцене плоскость, куб и сферу так, как показано на рисунке ниже. Создайте простой C# скрипт-файл и подключите его к сфере:

--------------------------------------------------------------------------------------------

Создаем на сцене три элемента
- Plane (Floor) с координатами (0, 0, 0)
- Cube (Target) с координатами (3, 0.5, 3)
- Sphere (RollerAgent) с координатами (0, 0.5, 0) и компонентом RigidBody

![image](https://user-images.githubusercontent.com/112868100/201082094-cb5605ec-350f-43c2-b9f9-271288e0678d.png)

--------------------------------------------------------------------------------------------

В папке проекта создаем новую папку Materials а которой соотвественно будут храниться материалы для наших объектов
- для RollerTarget - материал RollerTarget
- для Target - материал Target

![image](https://user-images.githubusercontent.com/112868100/201082734-181a3cf5-6f98-4e27-886f-7f7b8b96eb1f.png)

--------------------------------------------------------------------------------------------

Создаем пустой объект с названием TargetArea, и переносим наши объекты в него, для удобства взаимодействия (группировка)

![image](https://user-images.githubusercontent.com/112868100/201083082-90b65493-ee97-4bca-82f3-1b6a980e6b2b.png)

--------------------------------------------------------------------------------------------

- В скрипт-файл RollerAgent.cs добавьте код, опубликованный в материалах лабораторных работ – по ссылке.

--------------------------------------------------------------------------------------------

Создаем в папке проекта папку Scripts для наших будущих скриптов и в качестве компонента для RollerAgent добавляем скрипт с одноименным названием
Код для скрипта следующий:

```py
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8 - 4, 0.5f, Random.value * 8 - 4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);

        if (distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}
```

--------------------------------------------------------------------------------------------

- Объекту «сфера» добавить компоненты Rigidbody, Decision Requester, Behavior Parameters и настройте их так, как показано на рисунке ниже:

--------------------------------------------------------------------------------------------

В компонентах RollerAgent:
- Прикрепляем к значею Target объект Target
- Прикрепляем компонент Decision Requester
    - Decision Period = 10
- Прикрепляем компонент Behavior Parameters
    - Behavior Name = RollerBall
    - Space Size = 8
    - Continous Actions = 2
    
![image](https://user-images.githubusercontent.com/112868100/201086822-5ecc322e-1aaf-477a-984e-6b73b9c2819a.png)

--------------------------------------------------------------------------------------------

- В корень проекта добавьте файл конфигурации нейронной сети, доступный в папке с файлами проекта по ссылке.

--------------------------------------------------------------------------------------------

В корневой папке проекта создаем файл rollerball_config.yaml

![image](https://user-images.githubusercontent.com/112868100/201087487-fe79f1bc-99b8-4b3d-8ddf-4f32b498cfef.png)

--------------------------------------------------------------------------------------------

В него записать код из предложенного видеоматериала

```py
behaviors:
  RollerBall:
    trainer_type: ppo
    hyperparameters:
      batch_size: 10
      buffer_size: 100
      learning_rate: 3.0e-4
      beta: 5.0e-4
      epsilon: 0.2
      lambd: 0.99
      num_epoch: 3
      learning_rate_schedule: linear
    network_settings:
      normalize: false
      hidden_units: 128
      num_layers: 2
    reward_signals:
      extrinsic:
        gamma: 0.99
        strength: 1.0
    max_steps: 500000
    time_horizon: 64
    summary_freq: 10000
```

--------------------------------------------------------------------------------------------

- Запустите работу ml-агента

--------------------------------------------------------------------------------------------

Далее в консоли прописать команду 

```py
mlagents-learn rollerball_config.yaml --run-id=RollerBall --force
```

И проверить в Unity работу MLAgent

![image](https://user-images.githubusercontent.com/112868100/201093988-4c02dca6-91b3-438b-890d-1b9944487854.png)

--------------------------------------------------------------------------------------------

- Сделайте 3, 9, 27 копий модели «Плоскость-Сфера-Куб», запустите симуляцию сцены и наблюдайте за результатом обучения модели.

--------------------------------------------------------------------------------------------

Работа модели с 1-ой сценой:

![2022-11-10-17-45-11](https://user-images.githubusercontent.com/112868100/201096512-dcb4f683-c50c-4267-ab69-c32052552091.gif)

--------------------------------------------------------------------------------------------

Работа модели с 3-мя сценами:

![3](https://user-images.githubusercontent.com/112868100/201098247-b4f88378-952a-41ff-9fa0-dc2e1f0e91cd.gif)

--------------------------------------------------------------------------------------------

Работа модели с 9-ю сценами:

![9](https://user-images.githubusercontent.com/112868100/201098278-9b6335fb-4df6-4e42-9c16-c1be3b095e87.gif)

--------------------------------------------------------------------------------------------

Работа модели с 27-ю сценами

![27](https://user-images.githubusercontent.com/112868100/201098292-f654cba6-00da-4f16-bc48-5863bde9394a.gif)

--------------------------------------------------------------------------------------------

- После завершения обучения проверьте работу модели.

--------------------------------------------------------------------------------------------

Для проверки работы модели переносим файл RollerBall.onnx из результатов в assets, и переносим его в поле Model

![image](https://user-images.githubusercontent.com/112868100/201101721-81fb793a-4133-4e34-a9dd-266fdd9843f0.png)


![end](https://user-images.githubusercontent.com/112868100/201102094-842a9fb2-c9df-40ba-85d3-e49e1e28bc12.gif)


Выводы: С у увеличением количества моделей (учавствующих в каждой итерации одновременно), нейронная сеть быстрее обучается.

## Задание 2
###  Подробно опишите каждую строку файла конфигурации нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных на сфере.


### Behaviors
Описание поведения объекта

RollerBall
Имя объекта

trainer_type: ppo
Тип обучения с поощрением

hyperparameters
Гиперпараметры

batch_size: 10
Количество опытов на каждой итерации градиентного спуска. Это всегда должно быть в несколько раз меньше, чем buffer_size. Если вы используете непрерывные действия, это значение должно быть большим (порядка 1000). Если вы используете только дискретные действия, это значение должно быть меньше (порядка 10 секунд).

buffer_size: 100
Так как у нас trainer_type: ppo то данный параметр - это количество опыта, который необходимо собрать перед обновлением модели политики. Соответствует тому, сколько опыта должно быть собрано, прежде чем мы приступим к какому-либо изучению или обновлению модели. Это должно быть в несколько раз больше, чем batch_size. Обычно больший размер буфера соответствует более стабильным обновлениям обучения.

learning_rate: 3.0e-4
Начальная скорость обучения для градиентного спуска. Соответствует силе каждого шага обновления градиентного спуска. Обычно это значение следует уменьшить, если тренировка нестабильна, а вознаграждение постоянно не увеличивается. У нас стоит дефолтное значение.

beta: 5.0e-4
Сила регуляризации энтропии, которая делает политику "более случайной". Это гарантирует, что агенты должным образом исследуют пространство действий во время обучения. Увеличение этого параметра обеспечит выполнение большего количества случайных действий. Это должно быть скорректировано таким образом, чтобы энтропия (измеряемая с помощью TensorBoard) медленно уменьшалась вместе с увеличением вознаграждения.

epsilon: 0.2
Влияет на то, насколько быстро политика может развиваться во время обучения. Соответствует допустимому порогу расхождения между старой и новой политиками при обновлении с градиентным спуском. Установка этого малого значения приведет к более стабильным обновлениям, но также замедлит процесс обучения.

lambd: 0.99
Параметр регуляризации (лямбда), используемый при расчете обобщенной оценки преимущества (GAE). Это можно рассматривать как то, насколько агент полагается на свою текущую оценку стоимости при расчете обновленной оценки стоимости. Низкие значения соответствуют тому, что вы больше полагаетесь на текущую оценку стоимости (что может быть большим смещением), а высокие значения соответствуют тому, что вы больше полагаетесь на фактические вознаграждения, полученные в окружающей среде (что может быть большим отклонением). Параметр обеспечивает компромисс между ними, и правильное значение может привести к более стабильному процессу обучения.

num_epoch: 3
Количество проходов через буфер опыта при выполнении оптимизации градиентного спуска.Чем больше размер пакета, тем больше это допустимо сделать. Уменьшение этого параметра обеспечит более стабильные обновления за счет более медленного обучения.

learning_rate_schedule: linear
Определяет, как скорость обучения меняется с течением времени. Для PPO рекомендуется снижать скорость обучения до max_steps, чтобы обучение сходилось более стабильно. Однако в некоторых случаях (например, обучение в течение неизвестного периода времени) эта функция может быть отключена. Для trainer_type: ppo стоит дефолтное значение - linear.

network_settings:
Сетевые установки

normalize: false
Применяется ли нормализация к входным данным векторного наблюдения. Эта нормализация основана на текущем среднем значении и дисперсии векторного наблюдения. Нормализация может быть полезна в случаях со сложными проблемами непрерывного управления, но может быть вредной при решении более простых задач дискретного управления. В нашем случае стоит дефолтное значение.

hidden_units: 128
Количество единиц в скрытых слоях нейронной сети. Соответствует количеству единиц в каждом полностью связном слое нейронной сети. Для простых задач, где правильное действие представляет собой простую комбинацию входных данных наблюдения, это должно быть небольшим. Для задач, где действие представляет собой очень сложное взаимодействие между переменными наблюдения, это должно быть больше. Стоит дефолтное значение.

num_layers: 2
Количество скрытых слоев в нейронной сети. Соответствует тому, сколько скрытых слоев присутствует после ввода наблюдения или после кодирования CNN визуального наблюдения. Для простых задач меньшее количество слоев, скорее всего, будет обучаться быстрее и эффективнее. Для более сложных задач управления может потребоваться больше уровней. Стоит дефолтное значение.

reward_signals:
Этот раздел позволяет задать настройки как для внешних (т.е. основанных на окружающей среде), так и для внутренних сигналов вознаграждения (например, curiosity и GAIL).

extrinsic:
Эти настройки нужны, чтобы убедиться, что тренировочный прогон включает в себя сигнал вознаграждения, основанный на окружающей среде.

gamma: 0.99
Коэффициент дисконтирования для будущих вознаграждений, поступающих от окружающей среды. Это можно рассматривать как то, насколько далеко в будущем агент должен заботиться о возможных вознаграждениях. В ситуациях, когда агент должен действовать в настоящем, чтобы подготовиться к вознаграждению в отдаленном будущем, это значение должно быть большим. В тех случаях, когда вознаграждение является более немедленным, оно может быть меньше. Должно быть строго меньше 1.

strength: 1.0
Фактор, на который можно умножить вознаграждение, получаемое от окружающей среды. Типичные диапазоны будут варьироваться в зависимости от сигнала вознаграждения.

max_steps: 500000
Общее количество шагов (т.е. собранных наблюдений и предпринятых действий), которые должны быть выполнены в среде (или во всех средах, если используется несколько параллельно) до завершения процесса обучения. Если у вас есть несколько агентов с одинаковым именем поведения в вашей среде, все шаги, выполняемые этими агентами, будут способствовать одинаковому количеству max_steps.

time_horizon: 64
Сколько шагов опыта нужно собрать для каждого агента, прежде чем добавлять его в буфер опыта. Когда этот предел достигается до окончания эпизода, оценка стоимости используется для прогнозирования общего ожидаемого вознаграждения от текущего состояния агента. Таким образом, этот параметр балансирует между менее предвзятой, но более высокой оценкой дисперсии (длительный временной горизонт) и более предвзятой, но менее разнообразной оценкой (короткий временной горизонт).

summary_freq: 10000
Количество опыта, которое необходимо собрать перед созданием и отображением статистики обучения. Это определяет степень детализации графиков в Tensorboard.

Decision Requester
Компонент DecisionRequester автоматически запрашивает решения для экземпляра агента через регулярные промежутки времени. DecisionPeriod - период принятия решений. Частота, с которой агент запрашивает решение. Период принятия решения, равный 10, означает, что Агент будет запрашивать решение каждые 10 шагов.

Behavior Parameters
Параметры поведения класса. Компонент для настройки поведения экземпляра агента и его свойств. В параметрах поведения примера используется "Space Size" размером 8. Это означает, что вектор признаков, содержащий наблюдения Агента, содержит восемь элементов: компоненты x и z вращения куба агента и компоненты x, y и z относительного положения и скорости шара. В поле Continuous Action (непрерывные действия) стоит значение 2. Это нужно для управления количеством вращений x и z, которые он должен применять к себе, чтобы шар оставался сбалансированным.


## Выводы

В ходе лабораторной работы, я познакомился с программными средствами для организции передачи данных между инструментами google, Python и Unity. Научился взаимедействовать с помощью кода на языках C# и Python с Google таблицами. Узнал что такое API-ключ, ознакомился с основами работы в Console Cloud Google.

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
