# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Мосин Дмитрий Сергеевич
- РИ210936
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

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
Познакомиться с программными средствами для организции передачи данных между инструментами google, Python и Unity

## Постановка задачи.
В данной лабораторной работе на языке python будет реализован функционал, позволяющий генерировать стоимость товара (ресурса или игрового объекта) в виде набора данных. Созданный набор данных будет передан в google-таблицу с целью возможности дальнейшего их наглядного представляния и оптимизации. Также в этой лабораторной работе на движке Unity будет реализован функционал, позволяющий воспроизводить аудио-файлы со звуковой информацией в зависимости от значений входного набора данных из таблицы.
Позднее, в следующей лабораторной работе мы будем изменять стоимость указанного товара (ресурса или игрового объекта) через ML-агент. Далее стоимость товара будет меняться  в зависимости от прочих переменных (например, колличества собранного золота, скорости добычи сырья, скорости передвижения неигрового персонажа от рудника до города и пр). На основе указанных переменных мы научим ML-агент не выходить за пределы темпа инфляции.

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity. При выполнении задания используйте видео-материалы и исходные данные, предоставленные преподавателя курса.
Ход работы:
- В облачном сервисе google console подключить API для работы с google sheets и google drive.

Создаем новый проект в Console Cloud Google. Затем подключаем Google Sheets API и Google Drive Api из встроенного маркетплейса. После нам необходимо создать Service Account и указать в нем роль "Editor". 

![image](https://user-images.githubusercontent.com/112868100/195110035-a1220b81-b206-44a7-85c1-bef0f7dc03cb.png)

После этого нам нужно выгрузить API-ключ и созранить его в наш проект на PyCharm.

![image](https://user-images.githubusercontent.com/112868100/195110699-1c041dc0-fd69-48fa-94a1-eef16389ada1.png)

Далее нам необходимо скопировать email сгенерированный на нашем аккаунте, создать пустуой файл в сервисе Google таблицы, и добавить этот майл как пользователя-редактора

![image](https://user-images.githubusercontent.com/112868100/195111857-27c3c701-7cab-459b-9cc8-f057b0928a81.png)

В нашем проекте на Pycharm в Settings -> Project Interpretator устонавливаем пакет Google Spreadsheets Python API:

![image](https://user-images.githubusercontent.com/112868100/195113239-95647ce7-7f5c-46ea-bfa9-adedc7d5fb9b.png)

И пакет Numpy:

![image](https://user-images.githubusercontent.com/112868100/195113869-f75488ce-1a01-4fd1-9887-c4fb682036f8.png)


- Реализовать запись данных из скрипта на python в google-таблицу. Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период.

Пишем код как показано в видеоуроке от преподавателей:

```py
import gspread
import numpy as np
gs = gspread.service_account(filename='centering-talon-365213-6b629bd0007a.json')
sheet = gs.open('UnityData')
price = np.random.randint(2000, 10000, 11)
mon = list(range(1, 11))
i = 0
while i <= len(mon):
    i += 1
    if i == 0:
        continue
    else:
        temp_inf = ((price[i - 1] - price[i - 2]) / price[i - 2]) * 100
        temp_inf = str(temp_inf)
        temp_inf = temp_inf.replace('.', ',')
        sheet.sheet1.update(('A' + str(i)), str(i))
        sheet.sheet1.update(('B' + str(i)), str(price[i - 1]))
        sheet.sheet1.update(('C' + str(i)), str(temp_inf))
        print(temp_inf)
        
```
Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период.
Запустив программу, в консоли постепенно появляются числа, а так же они записываются в нашу Google таблицу:

![image](https://user-images.githubusercontent.com/112868100/195125592-c78e7144-2b63-4777-9cd7-e683d39f1b19.png)
![image](https://user-images.githubusercontent.com/112868100/195125642-d28994ba-9a29-4f9b-a4dd-fc7871294579.png)


- Создать новый проект на Unity, который будет получать данные из google-таблицы, в которую были записаны данные в предыдущем пункте.

Создаем API-key:

![image](https://user-images.githubusercontent.com/112868100/195126487-65c046ce-21db-4d0d-9de4-2ff518afde66.png)

Restrict key GoogleShhets API:

![image](https://user-images.githubusercontent.com/112868100/195127280-c9e032d7-a772-47ad-85b5-0fcaa2691dad.png)

В таблицах открываем общий доступ:

![image](https://user-images.githubusercontent.com/112868100/195127698-28d97366-c097-4b8a-b8d9-b2a8d77771ea.png)

Создаем 3D проект на Unity:

![image](https://user-images.githubusercontent.com/112868100/195127992-90994a54-aa62-43b7-b6bd-5f16423f89cd.png)

Импортируем два файла в наш проект "soundPackage.unitypackage" и "jsonPackage.unitypackage"

![image](https://user-images.githubusercontent.com/112868100/195139429-237cca89-d760-47a3-8cbd-0acfc6b15c80.png)

Создаем пустой объект и добавляем в него компонент "Audio source"

![image](https://user-images.githubusercontent.com/112868100/195141259-fbea220c-b3d9-46c4-9971-12e66730a573.png)

В добавленной папке "Script" создаем пустой скрипт, и открываем его

![image](https://user-images.githubusercontent.com/112868100/195141754-a1ded99f-5dad-4c8b-9932-b1c72cb33c50.png)
![image](https://user-images.githubusercontent.com/112868100/195141877-5dd18164-b7da-4b3d-a45b-e09ac6c39d43.png)

В файле пишем код по видеоуроку, не забывая о ссылке на нашу таблицу и ключе

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
    private Dictionary<string, float> dataSet = new Dictionary<string, float>();
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
        Debug.Log(dataSet["Mon_1"]);
    }

}
```

Запускаем, и видим, что значение в консоли совпадает со значением в таблице

![image](https://user-images.githubusercontent.com/112868100/195152505-75ac8447-ab87-4043-bfe4-0610095910d8.png)
![image](https://user-images.githubusercontent.com/112868100/195152573-56dd0bff-be60-415c-8186-5634afc84e2e.png)


- Написать функционал на Unity, в котором будет воспризводиться аудио-файл в зависимости от значения данных из таблицы.

Дописываем код по видеоуроку:

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
        if (dataSet["Mon_" + i.ToString()] <= 10 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 10 & dataSet["Mon_" + i.ToString()] < 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] >= 100 & statusStart == false & i != dataSet.Count)
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
}
```

Присваиваем переменным соотвествующие аудиодорожки

![image](https://user-images.githubusercontent.com/112868100/195160342-fa1a598d-7d14-4708-995c-19000dae2825.png)

Теперь в консоли выводятся все данные из Google таблицы и аудио-дорожка соотвествующая значению: 
- для значений меньше 10: "Люди восхищаются Вами, мой Лорд"
- для значений в диапозоне от 10 до 100: "Люди доверяют Вам, милорд"
- для значение больших 100: "Вы самый жестокий тиран в королестве, Ваша Светлость".

![image](https://user-images.githubusercontent.com/112868100/195160719-75a8e930-e4f3-41d6-823f-a1f30f56db1f.png)



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



## Задание 3

# Самостоятельно разработать сценарий воспроизведения звукового сопровождения в Unity в зависимости от изменения считанных данных в задании 2.

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
