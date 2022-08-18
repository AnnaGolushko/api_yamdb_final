## Проект YaMDb
Проект YaMDb собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха.
Произведению может быть присвоен жанр (Genre) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.

### Авторы проекта: 

**[Чернов Алексей](https://github.com/AlexBlackNn)**. Управление пользователями (Auth и Users): система регистрации и аутентификации, права доступа, работа с токеном, система подтверждения через e-mail.

**[Анна Руотси](https://github.com/Zizeka)**.  Категории (Categories), жанры (Genres) и произведения (Titles): модели, представления и эндпойнты для них.

**[Анна Голушко](https://github.com/AnnaGolushko)**. Отзывы (Review) и комментарии (Comments): модели, представления, настраивает эндпойнты, определяет права доступа для запросов. Рейтинги произведений.

### Cписок используемых технологий:
Django 

Django-rest-framework

### Как запустить проект:

Клонировать репозиторий и перейти в папку yatube_api

```
cd api_yamdb
```

Cоздать и активировать виртуальное окружение:

```
python3 -m venv env
```

```
source env/bin/activate
```

Установить зависимости из файла requirements.txt:

```
python3 -m pip install --upgrade pip
```

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python3 manage.py migrate
```

Запустить проект:

```
python3 manage.py runserver
```

### Последовательность загрузки данных важна!

Загрузить Пользователей в БД:

```
python manage.py load_users_data
```

Загрузить Жанры в БД:

```
python manage.py load_genre_data
```

Загрузить Категории в БД:
```
python manage.py load_category_data
```

Загрузить Произведения в БД:
```
python manage.py load_titles_data
```
Загрузить Ревью в БД:
```
python manage.py load_review_data
```
Загрузка Комментариев в БД
```
python manage.py load_comment_data
```

Загрузка связи Жанр Произведение 
```
python manage.py load_genre_title_data
```


Cоздать нового пользователя (в терминале появиться confirmation_code, например 619-f5cfa27f1dd04b07ba36)
```
POST http://127.0.0.1:8000/api/v1/auth/signup/
Content-Type: application/json

{
    "email": "Test_user@yamdb.fake",
    "username": "Test_user"
}
```

Передать пользователю токен (в терминале появиться {"token": "eyJ0eXAi.....})
```
POST http://127.0.0.1:8000/api/v1/auth/token/
Content-Type: application/json

{
    "confirmation_code": "619-f14dfe2a024b55d023a7",
    "username": "Test_user"
}
```

Запросить свою информацию
```
GET http://127.0.0.1:8000/api/v1/users/me/
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjU0MTg2NjAzLCJqdGkiOiI0MGE0ZjRlNTg2ZTI0MTJiYjYyN2JhZGJhODViZTk4YyIsInVzZXJfaWQiOjN9.AQAhyAWsR2_koog8ofuWy9QEWSSYObvI6C-VSbjIprE
```

Редактировать информацию о себе
```
PATCH http://127.0.0.1:8000/api/v1/users/me/
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjU0MTg2NjAzLCJqdGkiOiI0MGE0ZjRlNTg2ZTI0MTJiYjYyN2JhZGJhODViZTk4YyIsInVzZXJfaWQiOjN9.AQAhyAWsR2_koog8ofuWy9QEWSSYObvI6C-VSbjIprE

{
  "first_name": "Test",
  "last_name": "User",
  "bio": "Some biography1"
}
```
Получение списка всех пользователей.
В админке, нужно дать права админа (role) прежде!
```
GET http://127.0.0.1:8000/api/v1/users/
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjU0MTg2NjAzLCJqdGkiOiI0MGE0ZjRlNTg2ZTI0MTJiYjYyN2JhZGJhODViZTk4YyIsInVzZXJfaWQiOjN9.AQAhyAWsR2_koog8ofuWy9QEWSSYObvI6C-VSbjIprE
```

Получить пользователя по username.
```
GET http://127.0.0.1:8000/api/v1/users/Test_user/
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjU0MTg2NjAzLCJqdGkiOiI0MGE0ZjRlNTg2ZTI0MTJiYjYyN2JhZGJhODViZTk4YyIsInVzZXJfaWQiOjN9.AQAhyAWsR2_koog8ofuWy9QEWSSYObvI6C-VSbjIprE
```

Изменение данных пользователя по username
```
PATCH http://127.0.0.1:8000/api/v1/users/Test_user/
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjU0MTg2NjAzLCJqdGkiOiI0MGE0ZjRlNTg2ZTI0MTJiYjYyN2JhZGJhODViZTk4YyIsInVzZXJfaWQiOjN9.AQAhyAWsR2_koog8ofuWy9QEWSSYObvI6C-VSbjIprE

{
    "first_name": "string1",
    "last_name": "string2"
}
```