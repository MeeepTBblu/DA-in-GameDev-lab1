# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #4 выполнил(а):
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
Познакомиться с работой перцептрона на практике при помощи движка Unity. Реализовать перцептрон который умеет решать логические операции.



## Задание 1
### В проекте реализовать перцептрон, который умеет производить вычисления: OR, AND, NAND, XOR, и дать комментарии о кореектности работы.
----------------------------------------------------------------------------------------------------------------------------------------

### Ход работы:

(1) Первым неделом необходимо создать новый проект в Unity. Так как взаимодействовать мы будем только с консолью, неважно 2D или 3D проект мы создадим. Я выбрал 3D проект. В нем мы создаем пустой объект, на котором будет прекреплен скрипт работы парсептрона

![image](https://user-images.githubusercontent.com/100014698/205030038-c5b96de0-321f-4fd1-b1f9-bed9df1dd708.png)

----------------------------------------------------------------------------------------------------------------------------------------

(2) В папку проекта добавляем скрипт (Perceptron.cs) который уже написан преподавателями и предоставлен нам для выполнения лабораторной работы

``` py
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour
{

	public TrainingSet[] ts;
	double[] weights = { 0, 0 };
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2)
	{
		if (v1 == null || v2 == null)
			return -1;

		if (v1.Length != v2.Length)
			return -1;

		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;

		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights, ts[i].input);
		if (dp > 0) return (1);
		return (0);
	}

	void InitialiseWeights()
	{
		for (int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f, 1.0f);
		}
		bias = Random.Range(-1.0f, 1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for (int i = 0; i < weights.Length; i++)
		{
			weights[i] = weights[i] + error * ts[j].input[i];
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] { i1, i2 };
		double dp = DotProductBias(weights, inp);
		if (dp > 0) return (1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();

		for (int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for (int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start()
	{
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0, 0));
		Debug.Log("Test 0 1: " + CalcOutput(0, 1));
		Debug.Log("Test 1 0: " + CalcOutput(1, 0));
		Debug.Log("Test 1 1: " + CalcOutput(1, 1));
	}

	void Update()
	{

	}
}
```

----------------------------------------------------------------------------------------------------------------------------------------

(3) В данном скрипте нам достаточно взаимодействовать с методом **Train(int epochs)** - он влияет на количество эпох обучения пeрсептрона, и переменная **ts** с помощью которой мы будем задавать значения входа и выхода.

----------------------------------------------------------------------------------------------------------------------------------------

(4) Этот сприпт мы препляем на наш пустой объект.

![image](https://user-images.githubusercontent.com/100014698/205033412-19f8bc4e-301f-443d-befd-d4853d236bd9.png)

----------------------------------------------------------------------------------------------------------------------------------------

(5) В качестве входных и выходных значений мы зададим таблицу первой нужной нам логической операции OR

| A | B | A OR B |
| 0 | 0 |    0   |
| 1 | 0 |    1   |
| 0 | 1 |    1   |
| 1 | 1 |    1   |




















## Выводы

В ходе лабораторной работы, я познакомился с программными средствами для создания программы с машинным обучением. Познакомился с библиотеками -  mlagents и torch.
Научился взаимодействовать объектами, проводить итерации для машинного обучения и выводить результаты на объекты.
Познакомился с новыми компонентами объектов - Decision Requester, Behavior Parameters.

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
