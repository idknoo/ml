## Деревья решений

Цель: изучить применение дерева решений в рамках задачи регрессии  

Описание: нужно решить задачу регрессии. В качестве датасета необходимо взять данные о недвижимости 
Калифорнии из библиотеки sklearn.datasets. Целевая переменная – MedHouseVal.
На полученных данных построить модель регрессии и дерево решений.

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




### Этапы работы:

Обучили [модель регрессии](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html) на обучающем множестве.   
Обучили [дерево решений](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html) на обучающем множестве.  
Оптимизировали дерево решений, нашли наилучшие параметры max_depth & min_samples_leaf для данной модели деревьев.   
<br>

| Модель                                           | score | 
|--------------------------------------------------|-------|
| Linear regression                                | 0.596 |
| Decision tree                                    | 0.521 |   
| Decision tree (max_depth=7, min_samples_leaf=14) | 0.679 |  


Score стал намного лучше, когда мы отрегулировали всего 2 параметра. 

<hr>
<b>Вывод:</b> Линейная регрессия обычно быстро обучается, особенно на больших наборах данных, она подходит для задач с линейными зависимостями между признаками и целевой переменной.  
Деревья решений могут обучаться на разнообразных типах данных и моделировать сложные зависимости, не требуют предварительной нормализации данных, их легче визуализировать. Выбор модели зависит от конкретной задачи, данных и требований к интерпретируемости и производительности
<hr>






