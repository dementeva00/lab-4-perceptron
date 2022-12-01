Отчет по лабораторной работе #4 - "Перцептрон" выполнила:

Дементьева Юлия 
РИ-211002
Отметка о выполнении заданий (заполняется студентом):

Задание	Выполнение	Баллы
Задание 1	*	60
Задание 2	*	20
Задание 3	#	20
знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:

к.т.н., доцент Денисов Д.В.
к.э.н., доцент Панов М.А.
ст. преп., Фадеев В.О.
N|Solid

Build Status

Структура отчета

Данные о работе: название работы, фио, группа, выполненные задания.
Цель работы.
Задание 1.
Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
Задание 2.
Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
Выводы.
Цель работы
В проекте Unity реализовать перцептрон.

Задание 1
В проекте Unity реализовать перцептрон, который умеет производить вычисления: OR, AND, NAND, XOR, также дать комментарии о корректности работы.
Ход работы:

создала пустой 3D проект Unity "Perceptron"
скачала скрипт Perceptron.cs с репозитория и добавила его в свой проект.
![image](https://user-images.githubusercontent.com/114353535/205011988-55093064-1a16-43ac-a0cd-2d732e7fdeb6.png)

Содержание скрипта:
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
   public double[] input;
   public double output;
}

public class Perceptron : MonoBehaviour {

  public TrainingSet[] ts;
  double[] weights = {0,0};
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
     double dp = DotProductBias(weights,ts[i].input);
     if(dp > 0) return(1);
     return (0);
  }

  void InitialiseWeights()
  {
     for(int i = 0; i < weights.Length; i++)
     {
      weights[i] = Random.Range(-1.0f,1.0f);
     }
     bias = Random.Range(-1.0f,1.0f);
  }

  void UpdateWeights(int j)
  {
     double error = ts[j].output - CalcOutput(j);
     totalError += Mathf.Abs((float)error);
     for(int i = 0; i < weights.Length; i++)
     {			
      weights[i] = weights[i] + error*ts[j].input[i]; 
     }
     bias += error;
  }

  double CalcOutput(double i1, double i2)
  {
     double[] inp = new double[] {i1, i2};
     double dp = DotProductBias(weights,inp);
     if(dp > 0) return(1);
     return (0);
  }

  void Train(int epochs)
  {
     InitialiseWeights();

     for(int e = 0; e < epochs; e++)
     {
      totalError = 0;
      for(int t = 0; t < ts.Length; t++)
      {
       UpdateWeights(t);
       Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
      }
      Debug.Log("TOTAL ERROR: " + totalError);
     }
  }

  void Start () {
     Train(5); // сколько тренировок
     Debug.Log("Test 0 0: " + CalcOutput(0,0));
     Debug.Log("Test 0 1: " + CalcOutput(0,1));
     Debug.Log("Test 1 0: " + CalcOutput(1,0));
     Debug.Log("Test 1 1: " + CalcOutput(1,1));		
  }
}
Заполнила таблицу истинности для операции OR
![image](https://user-images.githubusercontent.com/114353535/205012347-8b1b370e-8384-4c5f-b356-fedb988135f4.png)

В резултате запуска проекта, отработав 5 эпох обучения, перцептрон научился безошибочно производить операцию OR
![image](https://user-images.githubusercontent.com/114353535/205012476-d5e22bfd-459b-49df-977e-18f80d129f7c.png)

Заполнила таблицу истинности для операции AND
![image](https://user-images.githubusercontent.com/114353535/205012729-192168ec-e842-4cbc-b2b6-3d7c5e4438ce.png)

В резултате запуска проекта, отработав 6 эпох обучения, перцептрон научился безошибочно производить операцию AND
![image](https://user-images.githubusercontent.com/114353535/205012829-829e13cf-49f9-49a0-9d3e-ca4221d7e045.png)

Заполнила таблицу истинности для операции NAND
![image](https://user-images.githubusercontent.com/114353535/205013083-9efb837a-ac9a-4d91-ac50-0ad407d7cde9.png)

В резултате запуска проекта, отработав 7 эпох обучения, перцептрон научился безошибочно производить операцию NAND
![image](https://user-images.githubusercontent.com/114353535/205013135-b54fdd5e-2113-42ae-ae5a-a4fc775be247.png)

Заполнила таблицу истинности для операции XOR
![image](https://user-images.githubusercontent.com/114353535/205013324-934c446c-a3fe-4006-87e4-695bd4e6fd06.png)

В этом случае перцептрон не сможет безошибочно производить вычисление операции XOR даже при 1кк эпох обучения, т.к. нейронная сеть с одним перцептроном может классифицировать только линейно-разделимые образы.

Задание 2
Построить графики зависимости количества эпох от ошибки обучения. 


Выводы
В результате проделанной работы я узнала о перцептроне: как он работает и какие задачи можно решать с помощью него.

Powered by
BigDigital Team: Denisov | Fadeev | Panov
