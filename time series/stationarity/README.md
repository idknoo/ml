## Временные ряды

Цель: узнать, что такое временные ряды, избавиться от нестационарности 

Имеется 6 датасетов:  
1. [daily-total-female-births-in-cal.csv](Series%2Fdaily-total-female-births-in-cal.csv)
   1. boxcox
   2. np.diff(series_1, 2)
2. [international-airline-passengers.csv](Series%2Finternational-airline-passengers.csv)
    1. np.diff(series_2, 1)
3. [mean-monthly-air-temperature-deg.csv](Series%2Fmean-monthly-air-temperature-deg.csv)
   1. boxcox
   2. np.diff(series_3, 1)
   3. series_3[12:] - series_3[:-12]
4. [monthly-boston-armed-robberies-j.csv](Series%2Fmonthly-boston-armed-robberies-j.csv)
   1. boxcox
   2. np.diff(series_4, 2)
5. [monthly-sales-of-company-x-jan-6.csv](Series%2Fmonthly-sales-of-company-x-jan-6.csv)
   1. np.diff(series_5, 1)
6. [weekly-closings-of-the-dowjones-.csv](Series%2Fweekly-closings-of-the-dowjones-.csv)
   1. np.diff(series_6, 1)

Стационарный ряд легче предсказать, можно предположить, что статистические свойства в будущем не изменятся

Интересные моменты:
1. Использование `series_3 = series_3[12:] - series_3[:-12`] и `series_3 = np.diff(series_3, 12)` дает разные результаты из-за различной логики вычислений  
Например:  
`col = np.array([10, 11, 12, 13, 14, 15, 20, 21, 22, 1])`
если сделать `col = col[2:] - col[:-2]`, то получится `2 2 2 2 6 6 2 -20`. Просто вычитаем с шагом 2 значения
`np.diff(col, 2)`  
при первой итерации (а у нас здесь их 2) получится `1 1 1 1 1 5 1 1 -21` (это то же самое, что и `diff(col, 1)`), а при второй итоговой `0 0 0 0 4 -4 0 -22`
2. Логарифм можно искать только от положительных чисел (`boxcox`)  
Box-Cox преобразование часто используется для стабилизации дисперсии или для придания данных нормального распределения. Однако оно может привести к проблемам, если в данных есть отрицательные значения или нули. Если ваши данные содержат такие значения, то Box-Cox преобразование может выдавать бесконечные значения или значения NaN после преобразования, что приведет к ошибке при дальнейшем анализе.

<hr>
<b>Вывод:</b> Таким образом, из имеющихся 6 нестационарных временных рядов, мы пришли к стационарности в каждом с помощью логарифмирования и дифференцирования. 
<hr>






