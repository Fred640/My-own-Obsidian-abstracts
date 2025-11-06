Django поддерживает PostgreSQL, MySQL, MariaDB, Oracle, SQLite. 
Django ORM (Object Relational Mapping) - компонент Django который позволяет обращаться к БД через классы python вместо sql запросов. Такой подход позволяет писать инвариантные sql запросы не привязываясь к конкретной СУБД. Также плюсом ORM является то что она сама закрывает БД когда пользователь покиадет сайт.

Для создания таблицы в бд нужно создать класс ORM c нужными полями, такие классы называются моделями. 
Все модели для приложения создаются в файле `<AppName>/models.py`

``
```
#<AppName>/models.py

class = <TableName>(models.Model):
	FieldName1 = models.FieldType(parameter1=..., parameter2=...)
	FieldName2 = models.FieldType(parameter1=..., parameter2=...)
	FieldName3 = models.FieldType(parameter1=..., parameter2=...)
```

#### Типы полей:
#### BooleanField - True/False
#### CharField - строковое поле для строк малого и среднего размеров
#### DataField - дата представленная в виде экземпляра класса datetime.date 
#### DateTimeField - дата представленная в виде экземпляра класса datetime.datetime
#### DecimalField - десятичное число с фиксированной точностью
#### DurationField - поле для хранения периода времени в виде экземпляра класса timedelta
#### EmailField - адрес электронной почты (будет проверен на действительность с помощью EmailValidator)
#### FilePathField - CharField ограниченный именами файлов в определенном каталоге файловой системы

