## Описание

API для Yatub - проект, представляющий из себя социальную сеть в которой воплощены возможности  
публикации и комментирования записей, а так же возможность подписываться или отписываться от авторов.

## Стек технологий

* Python 3.10,
* Django 4.4,
* DRF 3.12,
* JWT + Djoser 2.10

## Запуск проекта в dev-режиме

- Клонировать репозиторий
```bash
https://github.com/Overwhelmt/api_yatube.git
```

- Перейти в него

```bash
cd api_final_yatube
```

- Установите и активируйте виртуальное окружение c учетом версии Python 3.10:

```bash
python -m venv venv
```

```bash
source venv/Scripts/activate
```

```bash
python -m pip install --upgrade pip
```

```bash
cd yatube_api
```

```bash
pip install -r requirements.txt
```

- Выполняем миграции:

```bash
python manage.py migrate
```

- Создаем суперпользователя:

```bash
python manage.py createsuperuser
```

- Запускаем проект:

```bash
python manage.py runserver
```

## Примеры работы с API для всех пользователей

Для неавторизованных пользователей работа с API доступна в режиме чтения, что-либо изменить или создать не получится.

```r
GET api/v1/posts/ - получить список всех публикаций.
- при указании limit и offset выдача работает с разделением по странциами
GET api/v1/posts/{id}/ - получение публикации по id
GET api/v1/groups/ - получение списка доступных групп
GET api/v1/groups/{id}/ - получение информации о группе по id
GET api/v1/{post_id}/comments/ - получение всех комментариев к публикации
GET api/v1/{post_id}/comments/{id}/ - Получение комментария к публикации по id
```

## Примеры работы с API для авторизованных пользователей

- Для создания публикации используем:

```r
POST /api/v1/posts/
```

в body

```json
{
"text": "blablabla",
"image": "123dfjswofij1i3123jkdgbfijfwiouefjwcds",
"group": 0
}
```

- Обновление публикации:

```r
PUT /api/v1/posts/{id}/
```

в body

```json
{
"text": "blablabla",
"image": "123dfjswofij1i3123jkdgbfijfwiouefjwcds",
"group": 0
}
```

- Частичное обновление публикации:

```r
PATCH /api/v1/posts/{id}/
```

в body

```json
{
"text": "blablabla",
"image": "123dfjswofij1i3123jkdgbfijfwiouefjwcds",
"group": 0
}
```

- Удаление публикации:

```r
DEL /api/v1/posts/{id}/
```

Получение доступа к эндпоинту /api/v1/follow/ доступен только для авторизованных пользователей.

подписка пользователя от имени которого сделан запрос на пользователя переданного в теле запроса. Анонимные запросы запрещены.

```r
GET /api/v1/follow/
```

- Авторизованные пользователи могут создавать посты, комментировать их и подписываться на других пользователей.
- Пользователи могут изменять(удалять) контент, автором которого они являются.

## Добавить группу в проект нужно через админ панель Django:

после авторизации, переходим в раздел Groups и создаем группы.

```r
admin/
```

- Доступ авторизованным пользователем доступен по JWT-токену, который можно получить выполнив POST запрос по адресу:

```r
POST /api/v1/jwt/create/
```

- Передав в body данные пользователя (например в postman):

```json
{
"username": "blabla",
"password": "yaadminepepeepe"
}
```

- Полученный токен добавляем в headers (postman), после чего буду доступны все функции проекта:

```r
Authorization: Bearer {your_token}
```

- Обновить JWT-токен:

```r
POST /api/v1/jwt/refresh/
```

- Проверить JWT-токен:

```r
POST /api/v1/jwt/verify/
```

- Так же в проекте API реализована пагинация (LimitOffsetPagination):

```r
GET /api/v1/posts/?limit=5&offset=0
```
