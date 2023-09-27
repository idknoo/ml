## Feature Selection

Цель: изучить методы отбора признаков для эффективного обучения моделей машинного обучения

Описание: нужно решить задачу классификации точек наиболее эффективно. 
Для этого в работе необходимо применить различные методы по отбору признаков. 
Отбор признаков предпочтительнее осуществлять основываясь на математическом аппарате, 
поэтому данные для этого задания будут сгенерированы, чтобы избежать признаков с физическим смыслом.


### Этапы работы:

1. Сгенерировали данные с помощью кода:  
` from sklearn.datasets import make_classification
   x_data_generated, y_data_generated = make_classification(scale=1) `
2. Построли модель логистической регрессии и оцените среднюю точность.  
` cross_val_score(LogisticRegression(), x, y, scoring=‘accuracy’).mean()`
3. Использовали статистические методы для отбора признаков:  
a) Выберите признаки на основе матрицы корреляции.  
b) Отсеките низковариативные признаки (`VarianceThreshold`).
4. Осуществили отбор признаков на основе дисперсионного анализа:  
a) Выбрали 5 лучших признаков с помощью скоринговой функции для классификации f_classif (SelectKBest(f_classif, k=5)).  
5. Отобрали признаки с использованием моделей:  
a) Реализовали отбор признаков с помощью логистической регрессии.`SelectFromModel`.L1 регуляризация.  
b) Реализовали отбор признаков с помощью модели `RandomForest` и встроенного атрибута `feature_impotance`.
6. Реализовали отбор признаков перебором:  
a) `SequentialFeatureSelector`


| Способ выбора признаков                              | Количество признаков | Средняя точность модели |
| --------------------------------------------------- | ------------------- | ------------------------- |
| Базовая модель (все признаки)                        | 20                  | 0.90                    |
| Матрица корреляции                                   | 18                  | 0.90                    |
| VarianceThreshold                                     | 9                   | 0.94                    |
| Дисперсионный анализ (SelectKBest, f_classif)         | 5                   | 0.96                    |
| Отбор с использованием моделей (LogisticRegression)   | 8                   | 0.95                    |
| Отбор с использованием моделей (RandomForest)         | 5                   | 0.96                    |
| Перебор признаков (SequentialFeatureSelector)         | 5                   | 0.96                    |



<hr>
<b>Вывод:</b> Таким образом, заметим, что если мы будем использовать статические методы для отбора признаков, такие как матрица корреляции или 'как нам захочется, потому что нам кажется, что это сработает' не всегда может дать хороший результат. Конечно, на реальном датасете можно обосновывать, почему данный признак более или менее важен, но на искусственных данных мы убедились в том, что методы для отбора признаков справляются со своей задачей хорошо. Это можно и увидеть на показателях оценки точности. Не всегда количество признаков повышает точность.<br>
- Наилучшая средняя точность была достигнута с помощью методов отбора признаков, которые оставили только наиболее важные признаки (5 лучших) - это метод дисперсионного анализа и метод перебора признаков.<br>
- Отбор с использованием моделей также показал хорошие результаты, уменьшая размерность данных и улучшая среднюю точность.<br>
- Метод матрицы корреляции и VarianceThreshold оставили меньше признаков, но не сильно повысили точность модели<br>
- Важно учитывать, что выбор метода отбора признаков зависит от конкретной задачи и данных, и не всегда необходимо снижать размерность признакового пространства
<hr>





