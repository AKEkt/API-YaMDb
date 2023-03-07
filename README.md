# Проект Django REST Framework - YaMDb

## Мой учебный проект групповой разработки от @practicum-russia: проект YaMDb собирает отзывы пользователей на произведения. 

- #### Сами произведения в YaMDb не хранятся. 
- #### Добавлять произведения, категории и жанры может только администратор.
- #### Пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти. 
- #### Из пользовательских оценок формируется усреднённая оценка произведения — рейтинг.
- #### На одно произведение пользователь может оставить только один отзыв.
- #### Пользователи могут оставлять комментарии к отзывам.
- #### Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.


### Чтобы написать этот проект, мне нужно было:

- #### использовать библиотеку DRF;
- #### тестировать API через Postman;
- #### разобраться в сериализации, валидации, вьюсетах;
- #### применить регулярные выражения;
- #### применить аутентификацию по токену JWT;
- #### использовать проверка прав Permissions;
- #### групповая работа в GitHub.
  
## Инструменты и стек: #python #Git #GitHub #VSCode #Django #Postman #API #JWT #JSON #ReDoc

### Самостоятельная регистрация новых пользователей

- #### 1. Пользователь отправляет POST-запрос с параметрами email и username на эндпоинт /api/v1/auth/signup/.
- #### 2. Сервис YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на указанный адрес email.
- #### 3. Пользователь отправляет POST-запрос с параметрами username и confirmation_code на
  ####    эндпоинт /api/v1/auth/token/, в ответе на запрос ему приходит token (JWT-токен).

### Пользовательские роли

- ####  **Аноним** — может просматривать описания произведений, читать отзывы и комментарии.
- ####  **Аутентифицированный пользователь (user)** — может, как и **Аноним**, читать всё, 
     #### дополнительно он может публиковать отзывы и ставить оценку произведениям 
     #### (фильмам/книгам/песенкам), может комментировать чужие отзывы; может редактировать 
     #### и удалять свои отзывы и комментарии. Эта роль присваивается по умолчанию 
     #### каждому новому пользователю.
- ####  **Модератор (moderator)** — те же права, что и у **Аутентифицированного** 
     #### пользователя плюс право удалять любые отзывы и комментарии.
- ####  **Администратор (admin)** — полные права на управление всем контентом проекта. 
    #### Может создавать и удалять произведения, категории и жанры. Может назначать 
    #### роли пользователям.
- #### **Суперюзер Django** — обладает правами администратора (admin). Даже если 
    #### изменить пользовательскую роль суперюзера — это не лишит его прав администратора. 
    #### Суперюзер — всегда администратор, но администратор — не обязательно суперюзер.

### Ресурсы API YaMDb
- ####  Ресурс auth: аутентификация.
- #### Ресурс users: пользователи.
- #### Ресурс titles: произведения, к которым пишут отзывы (определённый фильм, книга или песенка).
- #### Ресурс categories: категории (типы) произведений («Фильмы», «Книги», «Музыка»). Одно 
  #### произведение может быть привязано только к одной категории.
- #### Ресурс genres: жанры произведений. Одно произведение может быть привязано к нескольким жанрам.
- #### Ресурс reviews: отзывы на произведения. Отзыв привязан к определённому произведению.
- #### Ресурс comments: комментарии к отзывам. Комментарий привязан к определённому отзыву.


## Запуск проекта в dev-режиме

- Клонировать репозиторий и перейти в него в командной строке:
```
git clone https://github.com/AKEkt/api_yamdb.git cd api_yamdb
```

- Cоздать и активировать виртуальное окружение:
```
    python3 -m venv env
    source env/bin/activate
```
- Установить зависимости из файла requirements.txt
```
    python -m pip install --upgrade pip
    pip install -r requirements.txt
```
- Выполнить миграции:
```
    python3 manage.py makemigrations
    python manage.py migrate
```

- В папке с файлом manage.py выполнить команду:
```
    git clone https://github.com/AKEkt/api_yamdb.git
    cd api_yamdb
```
- Для загрузки тестовых данных из csv-файлов выполнить команду:
```
    python3 manage.py load_base
```
### Примеры запросов для авторизованных пользователей
 Получение данных своей учетной записи:
```
Права доступа: user
GET api/v1/users/me/
```
Добавление категорий:
```
Права доступа: admin
POST /api/v1/categories/

{
  "name": "string",
  "slug": "string"
}
```
Добавление жанров:
```
Права доступа: admin
POST /api/v1/genres/

{
  "name": "string",
  "slug": "string"
}
```
Добавление произведений и обновление информации о произведении:
```
Права доступа: admin
POST /api/v1/titles/
PATCH /api/v1/titles/{titles_id}/

{
  "name": "string",
  "year": 0,
  "description": "string",
  "genre": [
    "string"
  ],
  "category": "string"
}
```
Удаление произведений
```
DELETE /api/v1/titles/{titles_id}/
```
Полный список эндпойнтов, методы и параметры запросов описаны в докуметации
к API и доступны по адресу:
```
http://127.0.0.1/redoc/
```

