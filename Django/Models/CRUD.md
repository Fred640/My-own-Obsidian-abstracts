Create
Read
Update
Delete

Все операции с бд можно выполнять с помощью Django ORM 

#### Create
###### Создать новую запись в таблице можно через консоль:
1) `python manage.py shell`  - открыть оболочку Django `python manage.py shell_plus --print-sql` - открыть оболочку с выводом sql запросов
2) `form <appName>/models import <ModelName>` — импортировать модель если еще не импортирована
3) `v1 = <ModelName>(Field1=... , Field2=...)` — создание экземпляра класса модели (еще не означает создание новой записи в таблице)
4) `v1.save()` - чтобы создать новую запись в таблице по экземпляру класса

######  Еще один способ добавления записи через консоль
1) `<ModelName>.objects.create(Field1=...)` — этот способ зразу добавит новый экземпляр класса в таблицу

#### Read
###### all()
`<ModelName>.objects.all()` — выведет все записи в консоль
этот вывод можно изменить добавив метод `__str__` в класс модели `<AppName>/models.py`
```
def __str__(self):
	return self.title
```
такой метод позволит при помощи команды `<ModelName>.objects.all()` получать названия каждой записи

`v = <ModelName>.objects.all()[0]` - Объявить переменную со значением первой записи в таблице. Затем `v` для вывода записи и `v.FiedName` - для вывода конкретного поля.

###### filter()
`<ModelName>.objects.filter(Field1="asd")` - получить записи у которых Field1=asd
К фильтру можно применять дополнительные методы сравнения помощью #lookups
`<ModelName>.objects.filter(Field1__<lookupName>="asd")`
`exact` - точное совпадение
`iexact` - точное совпадение без учета регистра
`contains` - проверка на содержание фрагмента
`icontains` - проверка на содержание без учета регистра
`in` - проверка, на то что поле точно совпадает с одним из значений списка `Entry.objects.filter(id__in=[1, 3, 4])`
`gt` - больше чем
`gte` - больше или равно
`lt` - меньше чем
`lte` - меньше или равно
`startswith` - начинается на (с учетом регистра)
`istartswith` - начинается на (без учета регистра)
`endswits` - заканчивается на (с учетом регистра)
`iendswits` - заканчивается на (без учета регистра)
`range` - в диапазоне от, до
`date` - принимает значение даты и позволяет использовать дополнительный lookup `Entry.objects.filter(pub_date__date__gt=datetime.date(2005, 1, 1))`
`yaer` - то же самое что и date только с годом
`month`
`week`
`day`
`week_day`
`time`
`hour`
`minute`
`second`
`isnull` - должно ли быть равно Null принимает True/False
`regex` - соответствие регулярному выражению с учетом регистра
`iregex` - соответствие регулярному выражению без учета регистра

в `filter` можно использовать #класс_Q который нужен для фильтрации запросов по нескольким условиям
`___.filter(Q(pk==3) | Q(isPublshed=0) & ~Q(cat_id__in=[1,2,3]))`
```
| - or
& - and
~ - not
```
в filter также есть #класс_F с помощью которого можно обращаться к значению поля записи например:
`___filter(F("pk")=F("cat_id"))`
`___update(id = f(id)+1)`
###### excluse - метод противоположный filter (вернет те записи которые не удовлетворяют условие)

###### get - всегда возвращает только одну запись (в нем нельзя прописывать lookups которые подразумевают выбор нескольких записей)
###### order_by - отсортирует выборку записей по какому-нибудь полю
например `Entry.objects.filter(id__in=[1, 3, 4]).order_by(title)`
чтобы изменить порядок сортировки на противоположный нужно перед `FieldName` поставить `-`

Такую же сортировку можно прописать в самой модели, создав подкласс `Meta`
```
class Meta:
	ordering = ['-time_create']
```

###### latest("timeFieldName") - вернет последнюю запись на основе заданного поля таблицы
###### earliest("timeFieldName") - вернет первую запись на основе заданного поля таблицы
###### get_previous_by
получить предыдущую запись по полю например `note.get_previous_by_time_create()`

###### get_next_by - противоположность get_previous_by
###### first
###### last
###### exists
###### count



###### Meta атрибуты #Meta_options
В модели можно создать подкласс Meta у него есть специальные атрибуты
`app_label` - если модель создана вне каталога приложения то в этом атрибуте описывается к какому приложению она относиться
`base_manager_name` - имя атрибута менеджера, например «objects», который будет использоваться для base_manager модели.
`db_table` - имя таблицы бд которое будет использоваться для модели
`db_table_comment` - комментарий для таблицы бд
`get_latest_by` - имя поля которое будет использоваться для методов latest() earliest()
`ordering` - дефолтная сортировка выборки записей по указанному полю
`indexes` - список полей которые будут индексированные

###### Пример получения и отображения на сайте данных из бд
метод get_object_or_404() - достает объект модели или если его нет возвращает исключение 404
```
#views.py
def post_show(request, post_id):
	post = get_object_or_404(Men, pk=post_id)
	data = {
		"title": post.title,
		"menu": menu,
		'post':post,
		"cat_selected": 1
	}
	return render(request, 'man/post.html', data)
	
#post.html
{% extends "base.html" %}
{% block content %}

<h2>{{post.title}}</h2>
{% if post.photo %}
<img class="img_article_left" src="{{post.photo.url}}">
{% else %}
<p>Нет фото</p>
{% endif %}
{{post.content|linebreaks}}

{% endblock content %}
```

Можно получить значение конкретного поля записи
`Model.objects.get(pk=1).title`
`Model.objects.get(pk=1).<FielName>`


#### Update
###### update - метод для обновления записей таблицы
`<ModelName>.oblects.update(FieldName=...)`
метод update можно использовать с всеми методами для чтения записей таблицы например
`<ModelName>.oblects.filter(pk__gte=4).update(FieldName=...)`
`<ModelName>.oblects.get(pk=4).update(FieldName=...)`
`<ModelName>.oblects.all().update(FieldName=...)`

#### Delete
delete - метод для удаления записей действует так же как и update