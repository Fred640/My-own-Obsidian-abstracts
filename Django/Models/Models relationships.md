w###### Типы связей:
*ForeignKey* - Many to One 
*ManyToManyField* - Many to Many
*OneToOneField* - One to One

###### on_delete
параметр который указываеться при создании связи между таблицами, значение которого влияет на действия СУБД при удалении записи из первичной таблицы
`models.CASCADE` - при удалении записи из первичной таблицы удаляются все связанные с ней записи из вторичной таблицы
`models.PROTECT` - запрещает удаление записи из перчиной таблицы если с ней связанны записи из вторичной таблицы
`models.SET_NULL` - при удалении записи из первичной таблицы устанавливеться `ForeignKey=NULL` для связанных с ней записей
`models.SET_DEFAULT` - при удалении записи из первичной таблицы устанавливеться `ForeignKey=<DefaultValue>` для связанных с ней записей
`models.DO_NOTHING` - ничего не менять во вторичной таблице при удалении записи в первичной
###### ForeigKey
Many to one - связь при которой записи из перчиной модели соответсвует несколько записей из вторичной модели (первичная модель - One, вторичная модель - Many)
Чтобы создать Mane to One связь между таблицами нужно в вторичной таблице создать поле `ForeignKey()`
```
class <seconModelName>(models.Model):
	KeyFieldName = models.ForeignKey("<FirstTableName>", on_delete=..., default=<defaultValue>)
```

![[screenshot_11112025_210430.jpg]]
Обращение к KeyField обьекта вторичной модели
`<ModelObject>.KeyField_id`

при связи Many to One можно обращаться к полям первичной таблицы через  обьект вторичной таблицы
`<ModelObject>.KeyFieldName.<FieldName>`

Можно получить доступ ко всем записям вторичной модели связанных  с записью первичной модели
`<FirstModelObject>.<secondModel>_set` - это менеджер запсей
!!! имя вторичной таблицы должно быть с маленькой буквы так как это метод `<secondModel>_set`
`<FirstModelObject>.<secondModel>_set.all()` - получить все записи вторичной модели связанне с записибю перчиной модели
к полям записи первичной модели связанной с записями из вторичной модели можно обращаться вот так
`<SecondModel>.objects.<KeyField>__<FirstFieldName>`



###### ManyToMany
ManyToMany - связь при кторой нескольким записям из первичной таблицы соответствует несколько записей из вторичной таблицы
Чтобы создать ManyToMany связь между моделями, нужно в вторичной модели создать поле MenyToManyField()
`ConnectingFieldName = models.ManyToManyField(to="<FirstModelName>")` - не имеет параметра on_delete
При создании такого поля в непосредственно в модель оно добавлено не будет, но будет создана отдельная таблица, в которой будут записываться все связи

![[screenshot_12112025_194455.jpg]]

связываение записи из вторичной таблицы с записями из первичной таблицы
`SecondModelNote.ConnectingFieldName.set([FirstModelNote1, FirstModelNote2, FirstModelNote3])`
Удаление связи
`SecondModelNote.ConnectingFieldName.remove([FirstModelNote1, FirstModelNote2, FirstModelNote3])`
Добавление связи
`SecondModelNote.ConnectingFieldName.add([FirstModelNote1, FirstModelNote2, FirstModelNote3])`
можно и наоборот `FirstModelNote.ConnectingFieldName.add([SecondModelNote1, SecondModelNote2, SecondModelNote3])`

Чтение связей
`SecondModelNote.ConnectingFieldName.all()`
