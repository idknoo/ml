## Работа с переменными

Цель: изучить применение методов разведочного анализа данных (EDA) для улучшения качества работы моделей машинного обучения

Описание: пулучшить метрики RMSE, R2 модели линейной регрессии путем работы с данными, 
а именно проведения разведочного анализа данных. В качестве датасета необходимо загрузить данные 
о недвижимости Калифорнии из библиотеки sklearn.datasets. Целевая переменная – MedHouseVal. 
Прочитать информацию о признаках датасета можно, выполнив следующий код – print(fetch_california_housing().DESCR)

### California Housing dataset
Описание датасета ['california_housing'](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.fetch_california_housing.html)

**Data Set Characteristics:**

- **Number of Instances:** 20640

- **Number of Attributes:** 8 numeric, predictive attributes and the target

**Attribute Information:**
- **MedInc:** Median income in block group
- **HouseAge:** Median house age in block group
- **AveRooms:** Average number of rooms per household
- **AveBedrms:** Average number of bedrooms per household
- **Population:** Block group population
- **AveOccup:** Average number of household members
- **Latitude:** Block group latitude
- **Longitude:** Block group longitude

**Missing Attribute Values:** None

This dataset was obtained from the StatLib repository. [Link to dataset](https://www.dcc.fc.up.pt/~ltorgo/Regression/cal_housing.html)

The target variable is the median house value for California districts, expressed in hundreds of thousands of dollars ($100,000).

This dataset was derived from the 1990 U.S. census, using one row per census block group. A block group is the smallest geographical unit for which the U.S. Census Bureau publishes sample data (a block group typically has a population of 600 to 3,000 people).

A household is a group of people residing within a home. Since the average number of rooms and bedrooms in this dataset are provided per household, these columns may take surprisingly large values for block groups with few households and many empty houses, such as vacation resorts.

It can be downloaded/loaded using the `sklearn.datasets.fetch_california_housing` function.

**References:**

- Pace, R. Kelley and Ronald Barry, Sparse Spatial Autoregressions, Statistics and Probability Letters, 33 (1997) 291-297




Этапы работы:

Проверили данные на наличие пропусков. Их не оказалось, но зато нашли огромное количество выбросов.  
Построили модель линейной регрессии. Вычислили метрики RMSE, R2 на обучающем и тестовом множестве.  
Построили график распределения целевой переменной.

Удалите признаки на основании корреляционной матрицы.
Исследовали оставленные признаки на выбросы.
Попытались удалить выбросы или сделать так, чтобы они помогали модели, а не сбивали ее. Поработали с переменным (возвели что-то в квадрат и тп)
  
Поставленная задача была довольно интересной и занимательной. Однако очень грустно от низких показателей метрик.


| Модель                                     | RMSE     | R²       | 
|--------------------------------------------|----------|----------|
| Модель 1: Все признаки                      | 0.731    | 0.616    |
| Модель 2: Коррелированные признаки          | 0.798    | 0.542   |    
| Модель 3: Коррелированные признаки без выбросов | 0.863    | 0.464    | 


<hr>
<b>Вывод:</b> Нууу, результаты довольно своеобразны. можно заметить, что как только мы усредняем значения или уменьшаем количество признаков, то модель от этого лучше не становится. Вообще, мне понравился этот датасет, слишком непонятные выбросы, которые сложно обосновать. Полиномизация значительно переобучает модель, поэтому ее использовать тоже не стоит. Было проведено много экспериментов, значительные результаты, где метрика R^2 была больше 0.60 не были показаны на данном датасете.
<hr>






