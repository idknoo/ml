## Улучшение качества модели

Цель: применить на практике алгоритмы по автоматической оптимизации параметров моделей машинного обучения.

Описание: нужно решить задачу классификации наличия болезни сердца у пациентов наиболее эффективно. 
Целевая переменная – наличие болезни сердца (HeartDisease). 
Она принимает значения 0 или 1 в зависимости от отсутствия или наличия болезни соответственно.

### Heart Failure Prediction Dataset

Описание датасета ['Heart Failure Prediction Dataset'](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction)

### Overview
Cardiovascular diseases (CVDs) are the number 1 cause of death globally, taking an estimated 17.9 million lives each year, which accounts for 31% of all deaths worldwide. Four out of 5 CVD deaths are due to heart attacks and strokes, and one-third of these deaths occur prematurely in people under 70 years of age. Heart failure is a common event caused by CVDs, and this dataset contains 11 features that can be used to predict a possible heart disease.

People with cardiovascular disease or who are at high cardiovascular risk (due to the presence of one or more risk factors such as hypertension, diabetes, hyperlipidaemia, or already established disease) need early detection and management wherein a machine learning model can be of great help.

### Attribute Information
- **Age:** Age of the patient [years]
- **Sex:** Sex of the patient [M: Male, F: Female]
- **ChestPainType:** Chest pain type [TA: Typical Angina, ATA: Atypical Angina, NAP: Non-Anginal Pain, ASY: Asymptomatic]
- **RestingBP:** Resting blood pressure [mm Hg]
- **Cholesterol:** Serum cholesterol [mm/dl]
- **FastingBS:** Fasting blood sugar [1: if FastingBS > 120 mg/dl, 0: otherwise]
- **RestingECG:** Resting electrocardiogram results [Normal: Normal, ST: having ST-T wave abnormality (T wave inversions and/or ST elevation or depression of > 0.05 mV), LVH: showing probable or definite left ventricular hypertrophy by Estes' criteria]
- **MaxHR:** Maximum heart rate achieved [Numeric value between 60 and 202]
- **ExerciseAngina:** Exercise-induced angina [Y: Yes, N: No]
- **Oldpeak:** Oldpeak = ST [Numeric value measured in depression]
- **ST_Slope:** The slope of the peak exercise ST segment [Up: upsloping, Flat: flat, Down: downsloping]
- **HeartDisease:** Output class [1: heart disease, 0: Normal]





### Этапы работы:

1. Категориальные переменные перевели в цифровые значения.
Разделили выборку на обучающее и тестовое подмножество. 80% данных оставить на обучающее множество, 20% на тестовое.
Обучили модель логистической регрессии с параметрами по умолчанию.
2. Подсчитайте основные метрики модели. Использовали следующие метрики и функцию:  
`cross_validate(…, cv=10, scoring=[‘accuracy’,‘recall’,‘precision’,‘f1’])`
3. Оптимизировали 3-4 параметра модели:
- Использовали GridSearchCV
- Использовали RandomizedSearchCV
- SVM
- KNN
4. Сравнили метрики

| Model                 | Best Parameters                          | Mean CV Score (GridSearchCV) | Mean CV Score (RandomizedSearchCV) |
|-----------------------|------------------------------------------|------------------------------|-----------------------------------|
| Random Forest         | `{'max_depth': 20, 'min_samples_leaf': 2, 'min_samples_split': 2, 'n_estimators': 100}` | 0.878716                    | 0.835424                          |
| SVM                   | `{'C': 1, 'kernel': 'linear'}`            | 0.847312                    | 0.847312                          |
| K-Nearest Neighbors   | `{'n_neighbors': 7, 'weights': 'distance'}` | 0.715564                    | 0.715564                          |


<hr>
<b>Вывод:</b> мы сравнили различные модели и нашли их лучшие параметры с помощью GridSearchCV и RandomizedSearchCV. Так как в RandomizedSearchCV значения берутся достаточно случайные, т.е. без определенного отступа, то найденные параментры могут не соответствовать параметрам в GridSearchCV. Лучше всего показал себя Random Forest с 'max_depth': 20, 'min_samples_leaf': 2, 'min_samples_split': 10, 'n_estimators': 50. 
<hr>






