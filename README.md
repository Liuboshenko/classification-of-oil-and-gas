# Классификация мест залежей нефти и газа

> Практическое задание №3 · Курс «Классическое машинное обучение» · НИЯУ МИФИ

---

## О проекте

Нефтегазовая отрасль предъявляет высокие требования к точности геологической разведки. Одна из ключевых задач — определить тип месторождения до начала дорогостоящего бурения: расположено ли оно **на суше** (ONSHORE), **в море** (OFFSHORE) или является **смешанным** (ONSHORE-OFFSHORE).

В рамках задания разработан алгоритм многоклассовой классификации, который по геологическим и географическим параметрам месторождения определяет его тип.

Соревнование на Kaggle: [classification-of-oil-and-gas](https://www.kaggle.com/competitions/classification-of-oil-and-gas)

**Лучший результат на публичном лидерборде: F1 = 0.92663**

---

## Что было сделано

| Этап | Описание |
|------|----------|
| **EDA** | Анализ структуры данных, пропусков, дисбаланса классов, корреляций числовых признаков |
| **Предобработка** | Удаление идентификаторов, заполнение пропусков (медиана/мода), Target Encoding для категориальных признаков |
| **Feature Engineering** | Создание признака `Lat_Long` (произведение координат) |
| **Балансировка классов** | `class_weight='balanced'` во всех моделях |
| **Пайплайны** | `sklearn.Pipeline` для корректного масштабирования внутри кросс-валидации |
| **Сравнение моделей** | LogisticRegression (baseline), RandomForest, GradientBoosting |
| **Подбор гиперпараметров** | `GridSearchCV` с 5-кратной стратифицированной кросс-валидацией |
| **Оценка важности признаков** | `feature_importances_` лучшей модели |
| **Предсказания** | Генерация файла submission для Kaggle |

---

## Структура проекта

```
classification-of-oil-and-gas/
│
├── solution_v6.ipynb              # Основной ноутбук с решением
│
├── train_oil.csv                  # Обучающая выборка (309 объектов)
├── oil_test.csv                   # Тестовая выборка (133 объекта)
│
├── submission_v6_GradientBoosting.csv  # Файл предсказаний для Kaggle
│
├── result_kagle.png               # Скриншот результата с лидерборда
├── setting_the_task.txt           # Текст задания
│
├── requirements.txt               # Зависимости проекта
├── python-version                 # Версия Python (3.12)
├── .gitignore
└── LICENSE
```

---

## Требования

- **Python 3.12**
- Все зависимости перечислены в `requirements.txt`

Ключевые библиотеки:

| Библиотека | Версия | Назначение |
|-----------|--------|------------|
| pandas | 3.0.2 | Работа с данными |
| numpy | 2.4.4 | Численные вычисления |
| scikit-learn | 1.8.0 | Модели, пайплайны, метрики |
| matplotlib / seaborn | 3.10.8 / 0.13.2 | Визуализация |
| xgboost | 3.2.0 | Gradient Boosting (расширенный) |
| lightgbm | 4.6.0 | Быстрый Gradient Boosting |
| catboost | 1.2.10 | Gradient Boosting с поддержкой категорий |
| imbalanced-learn | 0.14.1 | Методы балансировки классов |
| jupyterlab | 4.5.6 | Интерактивная среда разработки |

---

## Воспроизведение результатов

### 1. Клонировать репозиторий

```bash
git clone <url-репозитория>
cd classification-of-oil-and-gas
```

### 2. Создать виртуальное окружение

```bash
python3 -m venv venv3.12
```

### 3. Активировать окружение

```bash
# Linux / macOS
source venv3.12/bin/activate

# Windows
venv3.12\Scripts\activate
```

### 4. Установить зависимости

```bash
pip install -r requirements.txt
```

### 5. Запустить ноутбук

```bash
jupyter lab solution_v6.ipynb
```

Или выполнить все ячейки через nbconvert:

```bash
jupyter nbconvert --to notebook --execute --inplace solution_v6.ipynb \
    --ExecutePreprocessor.timeout=600
```

### 6. Результат

После выполнения всех ячеек в корне проекта появится файл:

```
submission_v6_<название_лучшей_модели>.csv
```

Этот файл готов для загрузки на Kaggle.

---

## Воспроизводимость

Для детерминированных результатов во всём коде зафиксирован `RANDOM_STATE = 42`.  
Все статистики предобработки (медиана, мода, средние для Target Encoding) вычисляются **только на обучающей выборке** и применяются к тестовой — утечки данных нет.

---

---

# Oil and Gas Fields Classification

> Practical Assignment #3 · Classical Machine Learning Course · NRNU MEPhI

---

## About

The oil and gas industry demands high precision in geological exploration. A key challenge is determining the **type of a field** before expensive drilling begins: is it located **onshore**, **offshore**, or is it a **mixed** type?

This project develops a multiclass classification model that predicts the field type based on geological and geographical parameters.

Kaggle competition: [classification-of-oil-and-gas](https://www.kaggle.com/competitions/classification-of-oil-and-gas)

**Best public leaderboard score: F1 = 0.92663**

---

## What Was Done

| Step | Description |
|------|-------------|
| **EDA** | Data structure analysis, missing values, class imbalance, numerical feature correlations |
| **Preprocessing** | Drop identifier columns, fill missing values (median/mode), Target Encoding for categorical features |
| **Feature Engineering** | Created `Lat_Long` feature (latitude × longitude product) |
| **Class imbalance** | `class_weight='balanced'` in all models |
| **Pipelines** | `sklearn.Pipeline` for leak-free scaling inside cross-validation |
| **Model comparison** | LogisticRegression (baseline), RandomForest, GradientBoosting |
| **Hyperparameter tuning** | `GridSearchCV` with 5-fold stratified cross-validation |
| **Feature importance** | `feature_importances_` from the best model |
| **Predictions** | Kaggle submission file generation |

---

## Project Structure

```
classification-of-oil-and-gas/
│
├── solution_v6.ipynb              # Main solution notebook
│
├── train_oil.csv                  # Training set (309 samples)
├── oil_test.csv                   # Test set (133 samples)
│
├── submission_v6_GradientBoosting.csv  # Kaggle submission file
│
├── result_kagle.png               # Leaderboard screenshot
├── setting_the_task.txt           # Assignment description
│
├── requirements.txt               # Project dependencies
├── python-version                 # Python version (3.12)
├── .gitignore
└── LICENSE
```

---

## Requirements

- **Python 3.12**
- All dependencies are listed in `requirements.txt`

---

## Reproducing Results

### 1. Clone the repository

```bash
git clone <repository-url>
cd classification-of-oil-and-gas
```

### 2. Create a virtual environment

```bash
python3 -m venv venv3.12
```

### 3. Activate the environment

```bash
# Linux / macOS
source venv3.12/bin/activate

# Windows
venv3.12\Scripts\activate
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Run the notebook

```bash
jupyter lab solution_v6.ipynb
```

Or execute headlessly via nbconvert:

```bash
jupyter nbconvert --to notebook --execute --inplace solution_v6.ipynb \
    --ExecutePreprocessor.timeout=600
```

### 6. Output

After all cells have been executed, a submission file will appear in the project root:

```
submission_v6_<best_model_name>.csv
```

This file is ready to be uploaded to Kaggle.

---

## Reproducibility

`RANDOM_STATE = 42` is fixed throughout the entire codebase.  
All preprocessing statistics (median, mode, target encoding means) are computed **exclusively on the training set** and then applied to the test set — no data leakage.
