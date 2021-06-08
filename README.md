### __Проект__:
## __Сайт-Блог "Yatube".__
` ` ` `
### __Цель проекта.__

Создание сайта с возможностью ведения публичного дневника, подписки на дневники других пользователей, добавления комментариев к записям дневника.

### __Содержание проекта.__

Стек:
Язык: Python 3.6.9.
Back-end: Django 2.2.6, SQLite.
Front-end: Bootstrap.
Тестирование: Unittest.

### __Функционал проекта.__

1. Установка интерфейса администратора сайта (админка).
 - создание суперпользователя (администратора)
 - регистрация в админке моделей Post и Group (описание моделей см.ниже) для возможности администрирования сообществ и постов пользователей (создание/редактирование/удаление).
 - реализация системы поиска и фильтрации в админке.

2. Создание и настройка форм регистрации и аутентификации пользователей.
Реализация возможности::
 - зарегистрироваться на сайте
 - пройти аутентификацию
 - сменить пароль.

3. Настройка авторизации пользователей.

    3.1. Неавторизованный пользователь может:
     - просматривать посты всех пользователей
     - просматривать комментарии к постам.
     - просматривать профиль сообщества

    3.2. Авторизованный пользователь может.
     - просматривать посты всех пользователей
     - просматривать комментарии к постам.
     - просматривать профиль сообщества
     - создавать пост (с указанием/без сообщества)
     - редактировать собственный пост
     - комментировать посты  свои и других авторов
     - редактировать свои комментарии
     - удалять свои комментарии
     - подписываться/отписываться от других авторов


4. Настройка пагинации:
 - на главной странице
 - на странице сообщества
 - в админке (в разделе постов)

### __Структура проекта.__

__Модели данных (Сущности).__

Модель _User_.
Модель _Post_
Модель Group
Модель Comment
Модель Follow

__Структуры моделей.__

Модель _User_.
Стандартная модель _User_, встроенная во фреймворк Django.

Модель _Post_.
 - _author_ - внешний ключ,  обязательное поле, связь Many-To-One с моделью _User_, содержит идентификатор пользователя.
 - _pub_date_ - обязательное поле, содержит дату и время создания поста.
- _text_  - обязательное поле, содержит текст поста.
- _group_ - внешний ключ,  обязательное поле, связь Many-To-One с моделью _Group_, содержит идентификатор названия сообщества (группы), где будет опубликован пост.
 - _image_ - необязательное поле для загрузки изображения к посту.

Модель _Group_.
 - _title_ - обязательное поле, содержит название сообщества.
 - _slug_ - обязательно поле, содержит уникальный ярлык сообщества.
 - _description_ - обязательное поле, содержит описание сообщества.

Модель _Comment_.
 - _post_ - внешний ключ,  обязательное поле, связь Many-To-One с моделью _Post_, содержит идентификатор поста.
 - _author_ - внешний ключ,  обязательное поле, связь Many-To-One с моделью _User_, содержит идентификатор пользователя.
 - _text_ - обязательное поле, содержит текст комментария.
 - _created_ - обязательное поле, содержит дату и время создания комментария.

Модель _Follow_.
 - _user_ - внешний ключ,  обязательное поле, связь Many-To-One с моделью _User_, содержит идентификатор пользователя (подписчика).
 - _author_ - внешний ключ,  обязательное поле, связь Many-To-One с моделью _User_, содержит идентификатор пользователя (автора).

![](https://github.com/abduev/Screenshots/blob/main/Yatube_DB.jpg/200x100)


### __Установка__.

1. Клонируйте проект с помощью git clone
2. Перейдите в папку с проектом и создайте виртуальное окружение.
_python3 -m venv venv_
3. Установите все необходимые пакеты.
_pip install -r requirements.txt_
4. Сделайте миграции
_python manage.py makemigrations_
_python manage.py migrate_
5. Создайте переменную окружения с помощью библиотеки dotenv.
Для переменной SECRET-KEY из settings Django-проекта, необходимо указать переменную окружения. Создайте файл .env и в нем создайте переменную DJANGO_SECRET_KEY и присвойте ей ключ, указав его в кавычках. Ключ удобно сгенерировать в онлайн сервисах, либо следующим способом:
```
    from django.core.management import utils


    print(utils.get_random_secret_key())
```

6. Запустите проект.
_python manage.py runserver_
7. Откройте в браузере адрес [http://127.0.0.1:8000](http://127.0.0.1:8000).
8. Можете скачать готовую базу с записями дневника Льва Толстого.
[https://code.s3.yandex.net/backend-developer/learning-materials/db.sqlite3.zip](https://code.s3.yandex.net/backend-developer/learning-materials/db.sqlite3.zip)
Скачайте файл, извлеките его из архива и замените им ваш файл db.sqlite3. Вместо вашей БД у вас будет база, заполненная тестовыми постами.
8. Создайте суперпользователя.
_python manage.py createsuperuser_
