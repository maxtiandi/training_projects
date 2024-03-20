# Определение токсичных комментариев (BERT)
Интернет-магазин «Викишоп» запускает новый сервис. Теперь пользователи могут редактировать и дополнять описания товаров, как в вики-сообществах. То есть клиенты предлагают свои правки и комментируют изменения других. Магазину нужен инструмент, который будет искать токсичные комментарии и отправлять их на модерацию.


---

**КОНТЕКСТ ИССЛЕДОВАНИЯ:**  набор данных с разметкой о токсичности правок

---

**ЦЕЛЬ ИССЛЕДОВАНИЯ:** обучить модель классифицировать комментарии на позитивные и негативные.

---

**КРИТЕРИИ УСПЕХА И ПРИМЕЧАНИЯ:**

- Значение метрики качества **F1** не меньше 0.75

---

**Описание данных для первого исследования:**

- *Данные:*  `/datasets/toxic_comments.csv` 

*Столбец text в нём содержит текст комментария, а toxic — целевой признак*

---
# Вывод
**В ходе исследования была выбрана и обучена лучшая модель, способная классифицировать комментарии на положительные и негативные**

- Изначальные данные в хорошем состоянии, предобработка не понадобилась
- Токенизировали данные при помощи предобученной модели BERT, специализирующейся на токсичных комментариях (взята из Toxic контеста)
- Перебрали гиперпараметры 4-х моделей, проверили усредненное качество метрики `F1-меры` на кросс-валидации:
    - `CatBoostClassifier` - лидер, со значением F1 на cross_val = **0.957883**
    - `XGBClassifier` - *0.953041*
    - `LGBMClassifier` - *0.952486*
    - `LogisticRegression` - *0.947330*

- `F1` лучшей модели на тестовой выборке: **0.93734335839599**

Конечный результат получился выше критерия успеха заказчика - получили отличное значение метрики :) 