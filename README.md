# Cup IT 2023 
## Ранжирование комментариев с помощью ML 
![Пасхалка](https://user-images.githubusercontent.com/115157179/226173708-39a4a6ca-098c-4c30-a032-a3dd056ab4cb.png)

## Состав команды:
- Наумовская Анастасия
- Абабков Роман
- Николаев Иван
- Староверов Максим
- Габитов Тимур

## Постановка задачи
Предложите механизм сортировки комментариев к постам по их популярности на основе методов 
машинного обучения, чтобы модель могла как можно лучше ранжировать пользовательские комментарии

- Проведите проверку и разведочный анализ данных (EDA) и подумайте, какие готовые решения можно 
использовать для представления текста.
- Используя тренировочную и тестовую выборки датасета, обучите модель ранжировать текстовые комментарии в порядке их популярности (от популярных к менее популярным) и проведите валидацию 
своей модели. Выбор модели необходимо аргументировать, основываясь на результатах обучения.
- Проанализируйте полученные результаты и сформулируйте полезные инсайты о том, что обычно содержит популярный комментарий, чтобы команда VK могла использовать эту информацию для улучшения комментариев своих пользователей.
- Предложите методы взаимодействия с комментаторами, а также механизмы поддержки для разных 
групп пользователей, включая тех, чьи комментарии непопулярны. 

## Структура решения

- **New_features_from_df**
> Выделяем новые фичи на основе комментариев и текстов постов
> анализируем влияние сгенерированных фичей на score
> Фичи для комментариев: len_with_spaces (длина комментариев, деленная по пробелам), links (индикатор содержания ссылки), emoji (индикатор содержания спецсимволов &#x), money (индикатор содержания знака $), quotes (индикатор содержания цитирования), col_sentence (количество предложений), tokenized (выделение токенизированных слов), col_words (количество слов), punc_count (количество знаков препинания), avg_len_words (средняя длина слов), total_digits (общее количество цифр), total_letters (общее количество букв)
> Фичи для текста: len_with_spaces (длина комментариев, деленная по пробелам), links (индикатор содержания ссылки), emoji_pic (количество эмодзи, содержащиеся в тексте), money (индикатор содержания знака $), quotes (индикатор содержания цитирования), col_sentence (количество предложений), col_words (количество слов), punc_count (количество знаков препинания), avg_len_words (средняя длина слов), total_digits (общее количество цифр), total_letters (общее количество букв)
- **EDA_features**
> Общий анализ фич из текста и комментария, выделения инсайтов
- **BERT**
> Выборка одного батча данных (1000), удаление спецсимволов, стопслов, нормализация. Обучение предобученной нейронной сети для векторизации признаков. Классификация с помощью различных методов
- **CountVectorizer()**
> Векторизуем данные с помощью CountVectorizer() и одновременно с его же помощью удаляем стопслова, нормализуем и разбиваем на токены. Используем MultinomialNB для классификации, либо после применяем TFIDF-трансформер и классифицируем с помощью MultinomialNB
- **TFIDF**
> Удаление спецсимволов, стопслов, нормализация. Векторизуем предложения с помощью TFIDFVectorizer и с помощью различных классификатор оцениваем score
- **ranking_test_solution.jsonl**
> Заполненный score на тестовой выборке
- **Презентация решения**

### Общий вывод

В датасете присутствует большое количество данных, из-за чего возникает сложность в обработке и дальнейшем масштабировании модели. Данные методы были выбраны на основе того, что они чаще всего используются в индустрии, а значит их сочетание может привести к неплохоим результатам.
Наилучший результат показало сочетание выделение Фичей из комментариев + KNN, поэтому на этом методе и обрабатывался test.  
На основе предобученной модели обработки естeственного языка Bert + KNN классификатора можно было получить высокий score, однако данная модель не подходит для масштабирования.

Также были предложены инициативы для внедрения системы ранжирования комментариев ВКонтакте:
- Предварительный рейтинг в поисковой строке для еще не опубликованного комментария
- Создание отдельного сервиса для комментаторов

**NLP Hell Yeah!**
