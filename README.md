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

Далее в консоли прописать команду 

```py
mlagents-learn rollerball_config.yaml --run-id=RollerBall --force
```

И проверить в Unity работу MLAgent

![image](https://user-images.githubusercontent.com/112868100/201093988-4c02dca6-91b3-438b-890d-1b9944487854.png)

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































## Задание 2
### Реализовать запись в Google-таблицу набора данных, полученных с помощью линейной регрессии из лабораторной работы № 1. 


Очистим таблицу от наших данных, и перепишем код в соотвествии с заданием

![image](https://user-images.githubusercontent.com/112868100/195161496-9037bbc8-841d-43f2-8bf0-9f18e0997f31.png)


Большая часть кода (а именно функции) остаются без изменений, меняется только обработка итераций

```py
import numpy as np
import gspread

x = [3, 21, 22, 34, 54, 34, 55, 67, 89, 99]
x = np.array(x)
y = [2, 22, 24, 65, 79, 82, 55, 130, 150, 199]
y = np.array(y)

def model(a, b, x):
  return a*x + b

def loss_function(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  return (0.5 / num) * (np.square(prediction - y)).sum()

def optimize(a, b, x, y):
  num = len(x)
  prediction = model(a, b, x)
  da = (1.0 / num) * ((prediction - y) * x).sum()
  db = (1.0 / num) * ((prediction - y).sum())
  a = a - Lr * da
  b = b - Lr * db
  return a, b

def iterate(a, b, x, y, times):
  for i in range(times):
    a, b= optimize(a, b, x, y)
  return a, b

a = np.random.rand(1)
b = np.random.rand(1)
Lr = 0.0001

gc = gspread.service_account(filename='centering-talon-365213-6b629bd0007a.json')
sh = gc.open("Regression")


prev_loss = 0
for index in range(1, 11):
    a, b = iterate(a, b, x, y, index)
    prediction = model(a, b, x)
    loss = loss_function(a, b, x, y)
    diff_loss = abs(loss - prev_loss)
    
    sh.sheet1.update(('A' + str(index)), str(index))
    sh.sheet1.update(('B' + str(index)), str(loss))
    sh.sheet1.update(('C' + str(index)), str(diff_loss))
    print(f'{index})\t{loss}\t{diff_loss}')
    prev_loss = loss
```

![image](https://user-images.githubusercontent.com/112868100/195166810-e2cd9771-104c-433f-b082-1c2c8de8c1de.png)
![image](https://user-images.githubusercontent.com/112868100/195166839-8df32f6c-2dee-447b-b70d-de51012bb5c4.png)



## Задание 3.

### Самостоятельно разработать сценарий воспроизведения звукового сопровождения в Unity в зависимости от изменения считанных данных в задании 2.

```py
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string,float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

    // Start is called before the first frame update
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if (dataSet["Mon_" + i.ToString()] <= 1 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 1 & dataSet["Mon_" + i.ToString()] < 777 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] >= 777 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/12vWQZ3B0NlPQ5amR_TX8YlyQPzmuG5wf9i2bFTItiXw/values/Лист1?key=AIzaSyBzex2EJDWrRDwuE_F-36qc-8pM6mvfDao");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[2]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```
Теперь считываются данные из таблицы Регрессий
- для значений меньше 1: "Люди восхищаются Вами, мой Лорд"
- для значений в диапозоне от 1 до 777: "Люди доверяют Вам, милорд"
- для значение больших 777: "Вы самый жестокий тиран в королестве, Ваша Светлость".



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
