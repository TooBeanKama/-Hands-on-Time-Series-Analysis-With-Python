---
tags:
  - Time-series
  - python
  - Спринт
файл: "[[Hands-on Time Series Analysis With Python From Basics To Bleeding Edge TechniquePatel).pdf]]"
Авторы: B. V. Vishwas, Ashish Patel
github: https://github.com/Apress/hands-on-time-series-analylsis-python/tree/master
---
[[-Vishwas__Hands-on-Time-Series-Analysis-With-Python]]

# Chapter 1. Time-Series Characteristics

> [!TIP] Что такое временной ряд

Временной ряд (time series) — это набор точек данных (data points), которые хранятся с учетом их времени. 

> [!TIP] Что такое анализ временных рядов

Математический и статистический анализ, выполняемый на такого рода данных для обнаружения **скрытых закономерностей** (hidden patterns) и инсайтов (meaningful insight, называется анализом временных рядов (time-series analysis).

> [!TIP] Зачем мы моделируем временные ряды

Методы моделирования временных рядов используются, чтобы понять прошлые закономерности на основе данных и попытаться спрогнозировать будущую динамику. 

> [!TIP]  Три вида данных

Существуют различные **виды данных**, такие как 
+ структурированные (**structured**), 
+ полуструктурированные (**semistructured**) и 
+ неструктурированные (**unstructured**)
и каждый тип следует обрабатывать по-своему, чтобы получить максимальную информацию. 

В этой книге мы будем рассматривать данные временных рядов, структурированные таким образом, как
+ данные фондового рынка, 
+ погоды, 
+ уровня рождаемости, 
+ трафика, 
+ приложений для совместного использования велосипедов и т. д


## Types of Data
	+ Time-Series Data
	+ Cross-Section Data
	+ Panel Data/Longitudinal Data

> [!TIP]  Три типа данных
> + временные ряды (Time-Series Data)
> + перекрестные данные (Cross-Section Data)
> + Панельные / Лонгитьюдные данные (Panel Data/Longitudinal Data)

![[Pasted image 20240617215740.png]]

### Time-Series Data
> [!TIP]  Хронологический порядок

Временной ряд содержит точки данных, которые увеличиваются, уменьшаются или иным образом изменяются в хронологическом порядке за период. 

> [!TIP]  univariate time series

Временной ряд, который включает записи одного объекта или переменной, называется одномерным временным рядом. 

> [!TIP]  Multivariate time series

Если записи включают более одного признака или переменной, ряд называется многомерным временным рядом. 

> [!TIP]  continuous и  discrete.

Кроме того, временной ряд можно обозначить двумя способами: непрерывным или дискретным. 

В непрерывном временном ряду наблюдение за данными осуществляется непрерывно на протяжении всего периода:
+ данные о магнитудах землетрясений, 
+ речевых данных и т. д. 

На рисунке 1-2 показаны данные о землетрясениях, непрерывно измеряемые с 1975 по 2015 год.
![[Pasted image 20240617220905.png]]

В дискретных временных рядах наблюдение за данными осуществляется в определенное время или через равные промежутки времени, например
+ повышении или понижении температуры, 
+ курсах валют, 
+ данных о атмосферном давлении и т. д. 

###  Cross-Section Data
Перекрестные данные — это данные, собранные в определенный момент времени по нескольким предметам, например
+ цены закрытия определенной группы акций на определенную дату, 
+ опросы общественного мнения, связанные с выборами, 
+ уровень ожирения среди населения и т. д. 

Пример перекрестных данных:
![[Pasted image 20240617221206.png]]


### Panel Data/Longitudinal Data
Панельные данные/продольные данные содержат наблюдения за многочисленными событиями, собранными в течение различных периодов времени для одних и тех же людей. 

Это данные, которые периодически определяются количеством наблюдений в перекрестных единицах данных (cross-sectional data), таких как отдельные лица, компании или государственные учреждения. 

В Таблице 1-1 приведены примеры данных, доступных для нескольких людей в течение нескольких лет, где собранные данные включают доход, возраст и пол.
![[Pasted image 20240617221327.png]]

В Таблице 1-1 наборы данных A и B (с атрибутами дохода, возраста и пола), собранные на протяжении многих лет, относятся к разным людям. 

> [!TIP] Сбалансированные панельные данные

Набор данных A представляет собой описание двух людей, Аллена и Малиссы, за которыми наблюдали в течение трех лет (2016, 2017, 2018); это известно как сбалансированные панельные данные. 

> [!TIP] Несбалансированные панельные данные

Набор данных B называется несбалансированными панельными данными, поскольку данные не существуют по каждому человеку каждый год.


## Trend
	+ Detecting Trend Using a Hodrick-Prescott Filter
	+ Detrending a Time Series

> [!TIP] Тенденция - mean rate of change with respect to time

Тренд (Тенденция) — это закономерность, которая наблюдается в течение определенного периода времени и представляет собой **среднюю скорость изменения во времени**. 

> [!TIP]  Восходящий и нисходящий тренды

Тенденция обычно показывает тенденцию данных к увеличению/восходящему тренду или уменьшению/нисходящему тренду в долгосрочной перспективе. 

Не всегда обязательно, чтобы увеличение или уменьшение происходило в одном и том же направлении на протяжении данного периода времени. 

> [!TIP]   candlestick charts

Линия тренда также рисуется с использованием свечных графиков. 


### Detecting Trend Using a Hodrick-Prescott Filter
> [!TIP]  Фильтр Ходрика-Прескотта (HP) 


Фильтр Ходрика-Прескотта (HP) стал эталоном для избавления от трендовых движений в данных. 

Этот метод широко используется для эконометрических методов в прикладных макроэкономических исследованиях. 

Этот метод является непараметрическим и используется для преобразования временного ряда в тренд; 

это циклический компонент, которому не помогает экономическая теория или предварительная спецификация тенденций.

> [!TIP]  Настройка фильтра: степень сглаживания

Как и все непараметрические методы, фильтр HP в значительной степени зависит от параметра настройки, который контролирует степень сглаживания. 

Математически фильтр Ходрика-Прескотта записывается как задача минимизации следующей функции потерь:
![[Pasted image 20240618085544.png]]

![[Pasted image 20240618085557.png]]


#### Код для выделения тренда фильтром Ходрика-Прескотта
```
import pandas as pd
import matplotlib.pyplot as plt
import warnings
warnings.filterwarnings('ignore')
from statsmodels.tsa.filters.hp_filter import hpfilter

# загрузка датасета
file = 'dataset/India_Exchange_Rate_Dataset.xls'
df = pd.read_excel(file, index_col=0, parse_dates=True)

# применение фильтра Ходрика-Прескотта
exinus_cycle, exinus_trend = hpfilter(df['EXINUS'], lamb=1600)

# отрисовка результатов

# исходный ряд
df['EXINUS'].plot(figsize=(15,6)).autoscale(axis='x', tight=True)

# тренд
exinus_trend.plot(figsize=(15,6)).autoscale(axis='x', tight=True)

# циклическая компонента
exinus_cycle.plot(figsize=(15,6)).autoscale(axis='x', tight=True)
```

![[Pasted image 20240618085936.png]]

![[Pasted image 20240618085945.png]]

![[Pasted image 20240618085953.png]]
## Seasonality
+ Multiple Box Plots
+ Autocorrelation Plot
+ Deseasoning of Time-Series Data
+ Seasonal Decomposition
## Cyclic Variations
+ Detecting Cyclical Variations
## Errors, Unexpected Variations, and Residuals
## Decomposing a Time Series into Its Components


# 2. Data Wrangling and Preparation for Time Series
## Loading Data into Pandas
+ Loading Data Using CSV
+ Loading Data Using Excel
+ Loading Data Using JSON
+ Loading Data from a URL
## Exploring Pandasql and Pandas Side by Side
### Selecting the Top Five Records
### Applying a Filter
### Distinct (Unique)
### IN
### NOT IN
## Ascending Data Order
## Descending Data Order
## Aggregation
### GROUP BY
### GROUP BY with Aggregation
## Join (Merge)
### INNER JOIN
### LEFT JOIN
### RIGHT JOIN
### OUTER JOIN
## Summary of the DataFrame
## Resampling
### Resampling by Month
### Resampling by Quarter
### Resampling by Year
### Resampling by Week
### Resampling on a Semimonthly Basis
## Windowing Function
### Rolling Window
### Expanding Window
### Exponentially Weighted Moving Window
## Shifting
## Handling Missing Data
### BFILL
### FFILL
### FILLNA
### NTERPOLATE


# 3. Smoothing Methods
## Introduction to Simple Exponential Smoothing
## Simple Exponential Smoothing in Action
## Introduction to Double Exponential Smoothing
### Double Exponential Smoothing in Action
## Introduction to Triple Exponential Smoothing
### Triple Exponential Smoothing in Action


# 4. Regression Extension Techniques for Time-eries Data
## Types of Stationary Behavior in a Time Series
## Making Data Stationery
### Using Plots
### Using Summary Statistics
### Using Statistics Unit Root Tests
## Interpreting the P-value
## Kwiatkowski-Phillips-Schmidt-Shin Test
## Using Stationary Data Techniques
### Differencing
### Random Walk
### First-Order Differencing (Trend Differencing)
### Second-Order Differencing (Trend Differencing)
### Seasonal Differencing
### First-Order Differencing for Seasonal Data
### Second-Order Differencing for Seasonal Data
## Autoregressive Models
## Moving Average
## Autocorrelation and Partial Autocorrelation Functions
## Introduction to ARMA
### Autoregressive Model
### Moving Average
## [[Introduction to Autoregressive Integrated Moving Average.pdf]]



## Introduction to Seasonal ARIMA
### SARIMA in Action
## Introduction to SARIMAX
### SARIMAX in Action
## Introduction to Vector Autoregression
### VAR in Action
## Introduction to VARMA
### VARMA in Action

# 5. Bleeding-Edge Techniques

Introduction to Neural Networks
Perceptron
Activation Function
Binary Step Function
Linear Activation Function
Nonlinear Activation Function
Sigmoid
TanH
Rectified Linear Unit
Leaky ReLU
Parametric ReLU
Softmax
Forward Propagation
Backward Propagation
Gradient Descent Optimization Algorithms
Learning Rate vs. Gradient Descent Optimizers
Recurrent Neural Networks
Feed-Forward Recurrent Neural Network
Backpropagation Through Time in RNN
Long Short-Term Memory
Step-by-Step Explanation of LSTM
Peephole LSTM
Peephole Convolutional LSTM
Gated Recurrent Units
Convolution Neural Networks
Generalized CNN Formula
One-Dimensional CNNs
Auto-encoders
Summary

# 6. Bleeding-Edge Techniques for Univariate Time Series
Single-Step Data Preparation for Time-Series Forecasting
Horizon-Style Data Preparation for Time-Series Forecasting
LSTM Univariate Single-Step Style in Action
LSTM Univariate Horizon Style in Action
Bidirectional LSTM Univariate Single-Step Style in Action
Bidirectional LSTM Univariate Horizon Style in Action
GRU Univariate Single-Step Style in Action
GRU Univariate Horizon Style in Action
Auto-encoder LSTM Univariate Single-Step Style in Action
Auto-encoder LSTM Univariate Horizon Style in Action
CNN Univariate Single-Step Style in Ac
CNN Univariate Horizon Style in Action

# 7. Bleeding-Edge Techniques for Multivariate Time Series
LSTM Multivariate Horizon Style in Action
Bidirectional LSTM Multivariate Horizon Style in Action
Auto-encoder LSTM Multivariate Horizon Style in Action
GRU Multivariate Horizon Style in Action
CNN Multivariate Horizon Style in Action


# 8. Prophet
The Prophet Model
Implementing Prophet
Adding Log Transformation
Adding Built-in Country Holidays
Adding Exogenous variables using add_regressors(function

-----------

















### Detecting Trend Using a Hodrick-Prescott Filter
Фильтр Ходрика-Прескотта (HP) стал эталоном для избавления от трендовых движений в данных.

Метод непараметрический и используется для разделения временного ряда на
+ тренд (тенденция)
+ на циклический компонент


Как и все непараметрические методы, фильтр HP в значительной степени зависит от параметра настройки, который контролирует степень сглаживания.
![[Pasted image 20240412173727.png]]
![[Pasted image 20240412173744.png]]
![[Pasted image 20240412173754.png]]
![[Pasted image 20240412173805.png]]

### Detrending a Time Series
Detrending is the process of removing a trend from time-series data, or it mentions a change in the mean over time.

Methods to detrend time-series data:
+ Pandas differencing
+ SciPy signal
+ HP filter

#### Detrending Using Pandas Differencing
+ метод `diff()`
+ It can provide a period value to shift in order to form the difference
![[Pasted image 20240412173830.png]]
![[Pasted image 20240412173842.png]]

#### Detrending Using a SciPy Signal
+ A signal is another form of time-series data. 
+ Every signal either increases or decreases in a different order.
+ `Signal.detrend` is a submodule of SciPy that is used to remove a linear trend along an axis from data.
![[Pasted image 20240412173905.png]]

![[Pasted image 20240412173917.png]]

### Detrend Using an HP Filter

+ `Hpfilter` is a submodule of Statmodels that is used to remove a smooth trend
![[Pasted image 20240412173941.png]]
![[Pasted image 20240412173951.png]]
![[Pasted image 20240412174001.png]]
![[Pasted image 20240412174011.png]]
![[Pasted image 20240412174020.png]]






