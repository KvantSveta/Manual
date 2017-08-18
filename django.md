# Django

**создание проекта mysite**
```bash
django-admin startproject mysite
```

**запуск миграции**
```bash
python manage.py migrate
```

**запуск сервера**
```bash
python manage.py runserver
# http://127.0.0.1:8000/ 
python manage.py runserver 8080
# http://127.0.0.1:8080/ 
python manage.py runserver 0:8000
# http://0.0.0.0:8000/ 
```

**создание приложения (модуля) polls**
```bash
python manage.py startapp polls
```

**создание миграции для приложения polls**
```bash
python manage.py makemigrations polls
```

**вывод в консоль sql-команд для 0001-миграции**
```bash
python manage.py sqlmigrate polls 0001
```

**проверка миграции на ошибки**
```bash
python manage.py check
```

- Для создания миграции необходимо внести изменения в модель (models.py)
- Создание миграции (python manage.py makemigrations)
- Применение миграции (python manage.py migrate)

**создание суперпользователя**
```bash
python manage.py createsuperuser
```
