# Django 

to create any project with django :

- create venv to clean work like this code 

'python -m venv (the projects folder name )'

- need to active the venv with this code '.\scripts\activate'

- need to install django to create project with django like this code :

'pip install django==3.2'

- create project with django  , like this 'django-admin startproject (name) '
- need to active the server ,like this 'python mange.py runserver '
- not forget   the migrate  for the rest 



-------------------

## Variables & Filter in  DTL :



in views.py with the (def)  in return render.......we have 3 values :1- request 2- 

path the template 3- context like this : '{'name':'ahmad'} '

and to display  need to : in the html site >> ex :'

name ={{name}}''

```py
from django.shortcuts import render

# Create your views here.


def index(request):
    return render(request, 'pages/index.html', {'name': 'Ahmad', 'age': '29'})
# we can this :
# def index(request):
#    x = {'name': 'Ahmad', 'age': '29'})
  #  return render(request, 'pages/index.html',x )


def about(request):
    return render(request, 'pages/about.html')

```

----------------------------------------

## Filters:

to add filter need this : 

we have two type from filters 

1- has not value  ex : filter

2- has value  ex : filter : numbers ,str .....

```py
# ex : in the html site 
	name = {{name|capfirst}} # first letter  capital
	name = {{name|default:'not found'}}# value default when have not any values 
		name = {{name|slice:':8 or  5:'}}#to slice values
 		name ={{name|length}}# to count the items in values
        name ={{name|add : 'mazen' }}# to and any values of the comming values
        name ={{name|cut}}# to cut any items in values  or values from values 
         age ={{age|filesizeformat}}# to change values to values ex from KB to GB or MB
```

--------------

## Tags with DTL:

- {%extends 'base.html'%} >>> ex the base.html  to  all sites in the project 

- to use html code in the site has extends from base  need to  add this : '{% block  'any name ' %} {% endblock %}'  and in the base '{%block  ' the name most one' %}{%endblock%}'

- to add nav and footer need create folder 'parts ' in this folder create files for nav and footer .html  then in the base we make include this sites but they have place that  means like this :

  ```py
  {%extends 'base.html'%}
  {%include parts/nav.html%}
   {% block  'any name ' %}
    {% endblock %}
   {% include parts/footer.html%}
  ```

  ---------------------------------------

  ## for & if :

   if ex :

  ```python
  {% if name =='ahmad' %}
  	<p>Hello Ahmad </p>
  {% elif name == 'hadil'  %}
  	<p>Hello Hadil </p>
  {% elif name == 'alma' %}
  	<p>Hello Alma </p>
  {% else %}
  	<p> Not Found </p>
  	
  	
  {
  {%endif %}
  
  ```

--------------

for ex : 

```python
{% for x in name  %}
<p>{{x}}</p>
{% endfor %}

{% endblock content %}
```

----------------------

# add the static and media files : 

need to lern this from all situation  and methods  

here find we the old method :

when you have the forn-end go to the >

1-create static folder in the project folder 

2- in this folder can you all what you need from  css js  imges 

3- this folder most be active in the settings with  static line and we most add this code : 

```
STATIC_ROOT = os.path.join(BASE_DIR,'static')
STATICURL='/STATIC/'
STATICFILES_DIRS=[
os.path.join(BASE_DIR,'the project name/static')
]


```

4- go to the command line and add this code :

'python  manage.py collectstatic'

5- connect the css files with html files :

ex :

```python
{% load static %} # to load staitc 
!
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
        <link rel="stylesheet" href="{% static 'css/style.css'%}"> to add the css files to the html files 

</head>
<body>
    
    {% include "parts/nav.html" %}
    {% block content %}
    {% endblock content %}
    {% include "parts/footer.html" %}
    
</body>
</html>
```

## when need to the css edit go to the old static in the project file make your options  and then make collectstaic in command line 



-----------------------------------------

## add URL with DTL :

ex :  to make URL : {% url 'name the site' %}

```django
{% extends "base.html" %}
{% block content %}
<span><a href="{% url 'index' %}">Home</a></span>
<span><a href="{% url 'about' %}">About</a></span> 
{% comment %}
  bla bla bla bla 
{% endcomment %}

  
{% endblock content %}
```

## to add comments : '{% comment %} {%endcomment%}'

---------------------

-------------

-------------------

# Database : 

Models :  he is file in any apps in the project and from him  you write the data that you need save in the database .

ex : any product has name , price , title , tags ,descriptions , flag , !!!!!........

## when i with django i dont need 

ex : 

```python

from django.db import models

# Create your models here.


class product(models.Model):
    name = models.CharField(max_length=50)
    content = models.TextField(max_length = 10000)
    price = models.DecimalField(max_digits =6,decimal_places = 2)
    # upload_to = 'photos/%y%m/%d' to make folder with 3 places to year & month & day
    image =models.ImageField(upload_to = 'photos/%y/%m/%d')
    active = models.BooleanField(default=False)

```





## any edit in the models and will you him in the admin display  most makemigriton and migrate in the command line 

------------------------

# not forget active the apps in the settings.py 



-----------------

-----------------

design the  models for the apps and display they in the admin panel

to display what in the models in the admin panel most go  to the admin file in the app and add this :

1-  create superuser in the command line with this code :

'python manage.py createsuperuser' with this have name ,email ,passowrd 

2- to display what in the models need to make migrations in the command line and migrate !!!!!! important all edit in the models need this ' python manage.py makemigrations ' and then ' python manage.py migrate'

3- from the admin file in the app we can through him control  the admin panel 

```python
admin.py 

from django.contrib import admin 
from . models import (class name)

# register your models here .

admin.site.register(class name)


```

--------------------------------

## display the models  and what in the database  in the templates :

when all correct in the app from  ( urls from app ,urls from project,views AND WHAT HAVE IN ,,admin file )

then can we display the models and what in database in templates from this codes :

1- in views ' from . models import (class name)'

2- in views with the def  add the values like this :

- 

```python
from django.shortcuts import render

# Create your views here.


def product_list(request):
    return render(request,'products/product_list.html',#dic{'name':'ahmad'})
# {'product_list':product.objects.all()}
#      key   :  class name from models . object  
def product_detail(request):
    return render(request, 'products/product_list.html')

```

- in the template :

  ```django
  {% extends "base.html" %}
  
  
  
  
  {% block content %}
  {% for x in product_list %}
  	<p>{{x.name}}</p>
  	<p>{{x.content}}</p>
  	<p>{{x.price}}</p>
  {% endfor  %}
  
  
  
  {% endblock content %}
  ```

  

# last 10 min from 21
