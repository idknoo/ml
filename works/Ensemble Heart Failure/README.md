## Ансамблирование

Цель: применить на практике базовые ансамблевые методы

Описание: нужно решить задачу классификации наличия болезни сердца у пациентов.
Целевая переменная – наличие болезни сердца (HeartDisease), принимает значения 0 или 1 в зависимости от отсутствия или наличия болезни соответственно. 
(Подробнее о признаках можно прочесть в описании датасета на сайте. 
Для выполнения работы не обязательно вникать в медицинские показатели.)

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

1. Проанализировали датасет, перевели категориальные признаки в цифровые значения ([pd.get_dummies](https://pandas.pydata.org/docs/reference/api/pandas.get_dummies.html) or [preprocessing.LabelEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html)
2. Реализовали визуализацию, которая основана на исследуемых данных
3. Разделили выборку на обучающее и тестовое подмножество.     
Построили модели:  
a) [tree.DecisionTreeClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html)  
b) [ensemble.RandomForestClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)
4. Вывели метрики для тестового подмножества для каждой построенной модели с помощью metrics.classification_report.
5. Обучили бэггинг над моделью DecisionTreeClassifier() [ensemble.BaggingClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.BaggingClassifier.html) 
6. Обучили стекинг трех моделей [ensemble.StackingClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.StackingClassifier.html):   
a) [DecisionTreeClassifier()]((https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html))  
b) [RandomForestClassifier()]((https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html))  
c) [LinearSVC()](https://scikit-learn.org/stable/modules/generated/sklearn.svm.LinearSVC.html)  
7. Сформулировали выводы по проделанной работе и сравнили метрики



| Модель                 | Accuracy  | Precision | Recall    | F1 Score  |
|------------------------|-----------|-----------|-----------|-----------|
| Decision Tree          | 0.782609  | 0.860215  | 0.747664  | 0.800000  |
| Random Forest          | 0.880435  | 0.897196  | 0.897196  | 0.897196  |
| Linear SVC             | 0.586957  | 0.969697  | 0.299065  | 0.457143  |
| Bagging (Decision Tree)| 0.885870  | 0.921569  | 0.878505  | 0.899522  |
| Stacking Classifier    | 0.869565  | 0.910891  | 0.859813  | 0.884615  |

<hr>
<b>Вывод:</b> Для нас ложно отрицательные результаты (пропуск целевого класса) более критичны, то нам следует стремиться к повышению полноты (recall). В данном случае, важно минимизировать количество случаев, когда модель не обнаруживает сердечную недостаточность у пациентов, которые действительно нуждаются в медицинском вмешательстве.  
Таким образом, наилучший результат показывает Random forest. У него наивысшие показатели Recall and F1 score.   
Random forest включает в себя bagging и случайные подпространства (т.е. использование случайных признаков)
<hr>






