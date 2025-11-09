###### Типы связей:
ForeignKey - Many to One 
ManyToManyField - Many to Many
OneToOneField - One to One

###### on_delete
параметр который указываеться при создании связи между таблицами, значение которого влияет на действия СУБД при удалении записи из первичной таблицы
`models.CASCADE` - при удалении записи из первичной таблицы удаляются все связанные с ней записи из вторичной таблицы
`models.PROTECT` - запрещает удаление записи из перчиной таблицы если с ней связанны записи из вторичной таблицы
`models.SET_NULL` - при удалении записи из первичной таблицы устанавливеться `ForeignKey=NULL` для связанных с ней записей
`models.SET_DEFAULT` - при удалении записи из первичной таблицы устанавливеться `ForeignKey=<DefaultValue>` для связанных с ней записей
`models.DO_NOTHING` - ничего не менять во вторичной таблице при удалении записи в первичной
###### ForeigKey
Чтобы создать Mane to One связь между таблицами нужно в вторичной таблице создать поле `ForeignKey()`
```
class <seconModelName>(models.Model):
	KeyFieldName = models.ForeignKey("<FirstTableName>", on_delete=..., default=<defaultValue>)
```
