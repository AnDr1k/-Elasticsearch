# Використання клієнту Elasticsearch(.js)

# Установка ES

Для цього нам спочатку потрібно Java. Розробники рекомендують встановити версії Java новіше, ніж Java 8 update 20 або Java 7 update 55.
Дистрибутив ES доступний на сайті розробника. Після розпакування архіву потрібно запустити bin/elasticsearch.
Після установки і запуску перевіримо працездатність:

export ES_URL=localhost:9200

curl -X GET $ES_URL

Ми отримаємо приблизно таку відповідь:

![image](https://user-images.githubusercontent.com/61386231/111884743-34606b80-89cc-11eb-9e4d-b6693a56c5a7.png)

# Індексація

Додамо пост в ES:

#/ Додамо документ c id 1 типу post в індекс blog.
#/ Pretty вказує, що висновок повинен бути придатним для читання людиною.


PUT /blog/post/1?pretty
{
  "title": "Доповідь з ІПЗ",
  "content": "<p>Історія про довгу підготовку доповіді<p>",
  "tags": [
    "доповідь",
    "ІПЗ"
  ],
  "published_at": "2021-03-15T20:44:42+00:00"
}


Отримаємо таку відповідь серверу:

![image](https://user-images.githubusercontent.com/61386231/112749346-70965c00-8fca-11eb-965b-7e615f4df9c1.png)

ES автоматично створив індекс blog і тип post. Можна провести умовну аналогію: індекс - це база даних, а тип - таблиця в цій БД. Кожен тип має свою схему - mapping, також як і реляційна таблиця. Mapping генерується автоматично при індексації документа:

#/ Отримаємо mapping всіх типів індексу blog

GET /blog/_mapping?pretty

відповідь серверу:

![image](https://user-images.githubusercontent.com/61386231/112749395-cbc84e80-8fca-11eb-941c-2aa2d0dea70f.png)

Варто відзначити, що ES не робить різниці між поодиноким значенням і масивом значень. Наприклад, поле title містить просто заголовок, а поле tags - масив рядків, хоча вони представлені в mapping однаково.


