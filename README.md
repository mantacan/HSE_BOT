# Оглавление

- [1. Предисловие](#1-предисловие)
- [2. Структура проекта](#2-структура-проекта)
  - [2.1. Сборка и запуск](#21-сборка-и-запуск)
  - [2.2. Классы и методы](#22-классы-и-методы)

---

## 1. Предисловие

Для поиска локаций использована демо-версия API 2gis, предоставляющая 1000 тестовых запросов. При одновременном использовании бота большим количеством людей возможны задержки и проблемы с генерацией ссылок. Также могут возникнуть трудности с поиском баров для группы: бот ищет ближайшие бары/клубы в радиусе 5 км от геолокации участника или центральной точки группы.

В процессе разработки несколько раз менялась концепция бота, из-за чего в коде могут быть неиспользуемые или бесполезные функции/методы. Прошу понять и простить.

**Рабочая версия бота: @knad_bar_bot**  
**По всем вопросам/проблемам пишите в Telegram: @mantacan**

---

## 2. Структура проекта

### 2.1 Сборка и запуск

В проекте используется база данных PostgreSQL, развернутая в контейнере. Для её запуска выполните следующие команды:

```bash
docker run --name my_postgres -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 postgres
```

Для входа в контейнер выполните:

```bash
docker exec -it my_postgres psql -U postgres
```

После этого создайте базу данных и таблицы, используя скрипт из `databases/init_db.sql`.

После запуска контейнера и создания БД приступайте к установке зависимостей и сборке проекта.

Установка зависимостей:

```bash
pip install -r requirements.txt
```

Далее необходимо указать токен Telegram бота в файле `config.txt` и ключ API 2gis в `config.ini`.

Для запуска проекта используйте команду:

```bash
python develop/main.py
```

### 2.2 Классы и методы

Исходный код находится в директории `develop`.

#### `main.py`

Основной файл, запускающий бота.

#### `controller.py`

Содержит базовую логику работы бота и отвечает за отрисовку кнопок.

#### `search.py`

Выполняет поиск локаций, генерацию координат и ссылок на заведения.  
*Примечание*: генерация ссылок реализована через костыли, так как API 2gis не предоставляет возможность получить ссылку на заведение.

#### `location_manager.py`

Отвечает за запрос и обработку геолокации пользователя.

#### `database_manager.py`

Управляет взаимодействием с базой данных.

#### `group.py`

Ранее самый большой и сложный класс, который был неоднократно переработан и упрощён.