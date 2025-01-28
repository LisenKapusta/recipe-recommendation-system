# Рекомендательная система и извлечение ключевых ингредиентов из рецептов

## Описание проекта

В рамках этого учебного проекта студенты разработают рекомендательную систему для рецептов, которая будет учитывать текстовое описание и ингредиенты, а также систему извлечения ключевых ингредиентов из текстового описания и шагов приготовления. Проект включает в себя несколько задач, каждая из которых направлена на решение конкретной проблемы в области обработки естественного языка и машинного обучения.

Проект состоит из следующих этапов:
1. **Рекомендательная система на основе текстовых данных.**
2. **Извлечение ключевых ингредиентов (NER).**

---

## Рекомендательная система на основе текстовых данных

В рамках этого задания студенты разработают рекомендательную систему, которая будет предлагать похожие рецепты на основе текстового описания (`description`) и ингредиентов (`ingredients`). Рекомендации должны учитывать как текстовое описание, так и ингредиенты.

Проект состоит из следующих этапов:
1. Подготовка данных и их векторизация.
2. Построение модели рекомендательной системы.
3. Оценка качества рекомендаций.

---

## Этап 1: Подготовка данных и их векторизация

### Задачи
- **Предобработка текстовых данных:** Очистка текста от лишних символов, приведение к нижнему регистру, удаление стоп-слов.
- **Векторизация текста:** Использование методов TF-IDF, Word2Vec или Doc2Vec для преобразования текстовых данных в числовые векторы.
- **Объединение данных:** Создание единого представления данных, учитывающего как текстовое описание, так и ингредиенты.

---

## Этап 2: Построение модели рекомендательной системы

### Что нужно сделать
- **Выбор метода поиска ближайших соседей:** Использование k-NN или cosine similarity для поиска похожих рецептов.
- **Настройка гиперпараметров:** Подбор оптимальных значений параметров модели (например, количество соседей в k-NN).
- **Обучение модели:** Обучение модели на подготовленных данных.

---

## Этап 3: Оценка качества рекомендаций

### Метрики качества
### Для оценки качества рекомендаций в зависимости от выбранного метода можно использовать следующие метрики:
- **Косинусное расстояние (Cosine Similarity)**: Если используется метод, основанный на косинусном сходстве, можно вычислить среднее значение косинусного сходства между исходным рецептом и рекомендованными. Чем выше значение, тем более релевантны рекомендации.
- **Среднее расстояние между рецептами**: Если используется метод k-NN, можно оценить среднее расстояние между исходным рецептом и рекомендованными. Чем меньше расстояние, тем лучше рекомендации.

---

# Извлечение ключевых ингредиентов (NER)

## Описание проекта

В рамках этого задания студенты разработают систему извлечения ключевых ингредиентов из текстового описания (`description`) и шагов приготовления (`cooking_steps`). Задача осложняется тем, что ингредиенты могут быть упомянуты в разных формах и требуется понимание контекста.

Проект состоит из следующих этапов:
1. Подготовка данных и их разметка.
2. Построение модели для извлечения именованных сущностей.
3. Оценка качества извлечения.

---

## Этап 1: Подготовка данных и их разметка

### Задачи
- **Разметка данных:** Создание аннотированного датасета, где ключевые ингредиенты выделены в тексте. Для автоматической разметки используйте (`ingredients`)

##### Шаги для разметки:
1. **Определение сущностей**:
   - В вашем случае сущностями являются ингредиенты. Например, в тексте "Добавьте 2 яйца и 100 г муки" сущности — это "яйца" и "мука".
   - Каждая сущность должна быть помечена меткой, например, `ING` (ингредиент).

2. **Форматы разметки**:
   - **BIO-формат**: Каждый токен (слово) в тексте помечается одной из меток:
     - `B-ING` (Beginning): Начало ингредиента.
     - `I-ING` (Inside): Продолжение ингредиента.
     - `O` (Outside): Токен не является частью ингредиента.
   - Пример:
     ```
     Добавьте   O
     2          O
     яйца       B-ING
     и          O
     100        O
     г          O
     муки       B-ING
     ```


3. **Пример автоматической разметки**:
   - У вас есть список ингредиентов: `["яйца", "мука", "сахар"]`.
   - Вы ищете эти слова в тексте и помечаете их как `B-ING` или `I-ING`.


- **Предобработка текста:** Очистка текста от лишних символов, приведение к нижнему регистру, удаление стоп-слов.

#### Предобработка текста: лемматизация и стемминг

Для улучшения качества модели NER важно провести предобработку текста. Лемматизация и стемминг — это два основных метода нормализации текста.

##### Лемматизация:
- **Что это**: Приведение слова к его начальной форме (лемме). Например:
  - "яйца" → "яйцо"
  - "добавляя" → "добавлять"
- **Зачем нужна**: Лемматизация помогает унифицировать разные формы слова, что улучшает качество распознавания сущностей.
- **Инструменты**: Используйте библиотеки, такие как `spacy` или `nltk`.

##### Стемминг:
- **Что это**: Отсечение окончаний слов для получения основы. Например:
  - "яйца" → "яйц"
  - "добавляя" → "добавля"
- **Зачем нужен**: Стемминг менее точен, чем лемматизация, но работает быстрее. Он может быть полезен для предварительной обработки больших объемов текста.
- **Инструменты**: Используйте `nltk` или `SnowballStemmer`.

##### Когда использовать:
- **Лемматизация**: Если важна точность и контекст (например, для NER).
- **Стемминг**: Если важна скорость обработки, а точность не критична.
---

## Этап 2: Построение модели для извлечения именованных сущностей

### Что нужно сделать
- **Выбор модели:** Использование моделей CRF, BiLSTM или предобученных языковых моделей (например, BERT).
- **Настройка гиперпараметров:** Подбор оптимальных значений параметров модели.
- **Обучение модели:** Обучение модели на размеченных данных.

#### Дообучение модели NER на своих метках

Предобученные модели NER (например, BERT или spaCy) уже умеют распознавать некоторые типы сущностей (например, имена, даты, локации). Однако для вашей задачи (извлечение ингредиентов) потребуется дообучение модели на своих данных.

##### Шаги для дообучения:
1. **Подготовка данных**:
   - Убедитесь, что ваш датасет размечен в формате, поддерживаемом моделью.
   - Разделите данные на тренировочный, валидационный и тестовый наборы.

2. **Выбор модели**:
   - **spaCy**: Легко дообучается на новых данных. Поддерживает BIO-формат.
   - **BERT**: Современная модель, которая показывает высокое качество в задачах NER. Можно использовать библиотеку `transformers` от Hugging Face.

3. **Дообучение модели**:
   - Загрузите предобученную модель (например, `bert-base-multilingual-cased`).
   - Добавьте новый слой для классификации ваших меток (`B-ING`, `I-ING`, `O`).
   - Обучите модель на своих данных.

---

## Этап 3: Оценка качества извлечения

### Метрики качества
- **IoU (Intersection over Union):** Оценка перекрытия извлеченных ингредиентов с истинными.

---

## Полезные ресурсы

### Ресурсы и полезные ссылки
 - **Рекомендательные системы**
 - https://www.kaggle.com/code/ramzanzdemir/recommendation-systems-content-based-tf-idf
 - **Извлечение ключевых ингредиентов (NER)**
 - https://medium.com/ubiai-nlp/mastering-named-entity-recognition-with-bert-ca8d04b67b18
 - https://towardsdatascience.com/custom-named-entity-recognition-using-spacy-7140ebbb3718
 - **Предобработка текста**
 - https://habr.com/ru/companies/otus/articles/774498/


### Датасет
 - https://huggingface.co/datasets/d0rj/povarenok_recipes_detail





