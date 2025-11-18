Это инструмент для оптимизации сайта
###### Установка
1) `pip install django-debug-toolbar`
2) В файле `settings.py` в коллекции `INSTALLES_APPS` должна быть строка `django.contrib.staticfiles` и `STATIC_URL = 'static/'`
3) В коллекции `TEMPLATES` `'BACKEND': 'django.template.backends.django.DjangoTemplates'` и `'APP_DIRS': True`
4) В коллекцию `INSTALLES_APPS` добавить `'debug_toolbar'`
5) В коллекцию `MIDDLEWARE` добавить `"debug_toolbar.middleware.DebugToolbarMiddleware"`
6) Добавить коллекцию `INTERNAL_IPS = ['127.0.0.1']`
7) В фале `<ProjectName>/urls.py` в коллекцию `urlpatterns` добавить путь `path("__debug__/", include("debug_toolbar.urls"))`
если все сделано верно то появиться такая панель
![[screenshot_18112025_150954.jpg]]