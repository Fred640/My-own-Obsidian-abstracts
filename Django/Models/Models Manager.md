Дефолтный менеджер моделей это objects
для создания своего менеджера нужно в файле `<appName>/models.py`
создать новый класс с именем менеджера
```
#<appName>/models.py
class PublishedManager(models.Manager):                        #создаем класс дочерний для models.Manager
	def get_queryset(self):                                    #прописываем метод get_queryset - что он будет возращать то и будет возращать менеджер
		return super().get_queryset().filter(isPublished=1)    #super().get_queryset() - это метод базового класса который вернет все записи
		
		
class = <ModelName>(models.Model):
	FieldName1 = models.FieldType(parameter1=..., parameter2=...)
	FieldName2 = models.FieldType(parameter1=..., parameter2=...)
	FieldName3 = models.FieldType(parameter1=..., parameter2=...)
	
	published = PublishedManager()                             #Создаем новый менеджер для модели и присваиваем ему созданный менеджер
```

как только в модель был добавлен новый менеджер, дефолтный менеджер objects перестает существовать
чтобы этого избежать его тоже нужно добавить в модель

```
class = <ModelName>(models.Model):
	FieldName1 = models.FieldType(parameter1=..., parameter2=...)
	FieldName2 = models.FieldType(parameter1=..., parameter2=...)
	FieldName3 = models.FieldType(parameter1=..., parameter2=...)
	
	published = PublishedManager()
	objects = models.Manager()
```