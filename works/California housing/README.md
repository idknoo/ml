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
1. 



| Метод        | Точность | Время работы |
|:-------------|:--------:|:------------:|
| GD           |   0.85   |    0.1642    | 
| RMSProp      |   0.90   |    0.0345    |
| Nadam        |   0.85   |    0.0656    | 
<hr>
<b>Вывод:</b> У нас мало данных. Очень сложно понять насколько хороша модель, когда у тебя в тестовом наборе всего 20 наборов. А взять у обучения тоже нельзя, так как там и так 80 наборов. Проблема.   
Если говорить о методах оптимизации, то мне больше всего понравился Nadam, который быстро сходится, довольно точный (если его подкрутить, то он не будет уступать RMSProp + добавить побольше данных желательно (чтобы точно все оценить, а не только об этом говорить).   
GD (градиентный спуск) показал себя неплохо, как и должен был, но чувствуется, что он обучается очень долго. За 1000 итераций он так и не смог обучиться на 100%. Еще можно попробовать стохастический градиентный спуск.   
Если говорить о точности, то все модели почти одинаковы на данном наборе данных. Невозможно сделать каких-либо заключений, основываясь на полученные метрики точности.
<hr>






