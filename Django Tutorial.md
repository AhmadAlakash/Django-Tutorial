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

- like this we will this change to the relay  name how can we this ? 

  <img src="C:\Users\49157\OneDrive\الصور\Screenshots\2022-10-16.png" alt="2022-10-16" style="zoom:200%;" />

with add this function to models  :

```python
from distutils.command.upload import upload


from django.db import models

# Create your models here.


class product(models.Model):
    name = models.CharField(max_length=50)
    content = models.TextField(max_length = 10000)
    price = models.DecimalField(max_digits =6,decimal_places = 2)
    # upload_to = 'photos/%y%m/%d' to make folder with 3 places to year & month & day
    image =models.ImageField(upload_to = 'photos/%y/%m/%d')
    active = models.BooleanField(default=False)
	def __str__(self):
		return self.name or waht we will
```

---------------------------

to change the name in the admin panel  like this :

![1d](E:\1d.png)

we add class meta to the mother class :

```python
from distutils.command.upload import upload


from django.db import models

# Create your models here.


class product(models.Model):
    name = models.CharField(max_length=50)
    content = models.TextField(max_length = 10000)
    price = models.DecimalField(max_digits =6,decimal_places = 2)
    # upload_to = 'photos/%y%m/%d' to make folder with 3 places to year & month & day
    image =models.ImageField(upload_to = 'photos/%y/%m/%d')
    active = models.BooleanField(default=False)
	def __str__(self):
		return self.name or waht we will
	class Meta :
		verbose_name='bl bla bla '
```

<img src="C:\Users\49157\OneDrive\الصور\Screenshots\2022-10-16 (2).png" alt="2022-10-16 (2)" style="zoom:200%;" />

--------------

what can i to order the products ex : names ,  price ,content or with values (-) : -name , - price , -content any things :

with this class :

```python
from distutils.command.upload import upload


from django.db import models

# Create your models here.


class product(models.Model):
    name = models.CharField(max_length=50)
    content = models.TextField(max_length = 10000)
    price = models.DecimalField(max_digits =6,decimal_places = 2)
    # upload_to = 'photos/%y%m/%d' to make folder with 3 places to year & month & day
    image =models.ImageField(upload_to = 'photos/%y/%m/%d')
    active = models.BooleanField(default=False)
	def __str__(self):
		return self.name or waht we will
	class Meta :
        ordering=['name'] or ['price'] or ['-price']
		
```

--------------------------------

add default value for any fields in the ex models :



```python
from distutils.command.upload import upload


from django.db import models

# Create your models here.


class product(models.Model):
    name = models.CharField(max_length=50)
    content = models.TextField(max_length = 10000,default ='last time')
    price = models.DecimalField(max_digits =6,decimal_places = 2 default =10.5)
        image =models.ImageField(upload_to = 'photos/%y/%m/%d',default = '')# here need to add the path for image

		
```

--------------------

## null = True , blank = True

when user  will not image  or content or any fields to adding most we this by null = True , blank = True to make the filed not required  , like this :

```python
from distutils.command.upload import upload


from django.db import models

# Create your models here.


class product(models.Model):
    name = models.CharField(max_length=50)
    content = models.TextField(max_length = 10000,null = True, blank = True)
    price = models.DecimalField(max_digits =6,decimal_places = 2null = True, blank = True)
        image =models.ImageField(upload_to = 'photos/%y/%m/%d',null = True, blank = True)# here need to add the path for image

		
```



----------------

to change  the names in the admin panel but not in the models we add verbose_name to the filed that we need change  ex : 

```python
class product(models.Model):
    name = models.CharField(max_length=50 , verbose_name ='title')
    content = models.TextField(max_length = 10000,null = True, blank = True)
```

----------------------

to  add category to the models for the products : 

ex : 

```python
from distutils.command.upload import upload


from django.db import models

# Create your models here.


class product(models.Model):
	x = ('Phone','Phone'),('Computer','Computer')
    # here we add this one to admin panel and the another to the database
	category = models.CharField(max_length=50,choices = x ) # here most add the tuple or variable to work here make we variable x and add to choices to make dropdown
    name = models.CharField(max_length=50)
    content = models.TextField(max_length = 10000,null = True, blank = True)
    price = models.DecimalField(max_digits =6,decimal_places = 2null = True, blank = True)
        image =models.ImageField(upload_to = 'photos/%y/%m/%d',null = True, blank = True)# here need to add the path for image

		
```

## not forget the makemigratioms and migrate  in the command line to display what we new have in the models 

-----------------------------

we have more fields  and here learn about some of them 

## !!! not forget the edit in the admin file and in command line to see what we have new in models and in admin 

```python
class test (models-Model):
	date = models-DateField() # to date  
	Time = modles.TimeField(null=True) to time 
	Created_at = Modles.DateTime(null=True) to date and time 
```

--------------------

when we will the time and date now ex with user will account create or sign in in one from apps media any things !!!! 

for this we have more library's and here use  one example  : 

```python
from datetime import datetime # for date and time >> we can use .now to make live time 

from django.db import models

# Create your models here.


class product(models.Model):
	x = ('Phone','Phone'),('Computer','Computer')
    # here we add this one to admin panel and the another to the database
	category = models.CharField(max_length=50,choices = x ) # here most add the tuple or variable to work here make we variable x and add to choices to make dropdown
    name = models.CharField(max_length=50)
    content = models.TextField(max_length = 10000,null = True, blank = True)
    price = models.DecimalField(max_digits =6,decimal_places = 2null = True, blank = True)
        image =models.ImageField(upload_to = 'photos/%y/%m/%d',null = True, blank = True)# here need to add the path for image
    created_at = models.DateTime(default = datetime.now   ) # here have we 

		
```

----------------------------------

# !!!!     Relation ships between Tables !!!!!!!!!!! 

### very important : 

## all example virtual in the models,py  file

not forget the edit in the admin file to display  the new items in the app or what have you in the models.py new 

###  1- one to one :

```python
from django.db import models
# relations 
#- one to one 
class famale(models.Model):
	name = models.CharFiled(may_length=50)
	
	
	
class male (models.Model):
name = models.CharFiled(max_length=50)
girls = models.OneToOneFiled(female,on_delete =models.CASCADE)# CASCADE to delete all 				 PROTECT to delete just what here not the item in the relation

    # not forget command line and admin.py
										
        
```

## One To Many :

this example of the relation with one to many 

```python
from django.db import models
# relations 
#- one to many 
class product(models.Model):
	name = models.CharFiled(may_length=50)
	
	
	
class user (models.Model):
	name = models.CharFiled(max_length=50)
	product= models.ForeignKey(product,on_delete=models.CASCADE)						
        
```

------------------

## Many To Many :

this example of the relation many to many :#

```python
from django.db import models
# relations 
#- many to many 
class video(models.Model):
	name = models.CharFiled(may_length=50,video,null=True)
	
	
	
class user1 (models.Model):
	name = models.CharFiled(max_length=50,video,null=True)
	product= models.ManyTOMany(video,null=True)						
        
```







test the last edit and we with by 26 

---------------------

## 26 Django tutorial | how display products for the users from database | query set by get and filter and all :

### important !!!!! :

 now i will display the info  that in the database   in one table ex .product 

- import the class from model in the views.py to use this in the views 

- go to the function that need display in the templet 

- add context to the function  ex :

  ```python
  from django.shortcuts import render
  from . models import product
  
  # Create your views here.
  
  
  def product_list(request): #{ key can any things,  value  , objict is the product   and all to display all products }
      return render(request, 'products/product_list.html', {'product_list': product.objects.all()})
  dont forget we can add the value to variable and can we that easy using 
      
  
  
  def product_detail(request):
      return render(request, 'products/product_detail.html')
  
  ```

  then we go to the template and add loop ,we  most that make : 

  ```python
  {% extends "base.html" %}
  
  
  
  
  {% block content %}
  {% for x in product_list %}
  	<p>{{x.name}}</p>
  	
  	<p>{{x.content}}</p>
  	
  	<p>{{x.price}}</p>
  	<hr>
  {% endfor  %}
  
  
  {% endblock content %}
  ```

  

when i will just  one object display  i give the value get instead of all   ex :

```python
from django.shortcuts import render
from . models import product

# Create your views here.


def product_list(request):
    return render(request, 'products/product_list.html', {'product_list': product.objects.get()})# get take value :any value ex name, id , content 
    


def product_detail(request):
    return render(request, 'products/product_detail.html')

```

then go to the template and use the idea variables  in the dtl  ex :

```python
{% extends "base.html" %}




{% block content %}
<p>
{{product_list}}# when i display any thisngsfrom the object name, pirce ,content  {{product_list.name or .price }}
</p>

{% endblock content %}
```

------------------

when i will not one and not all but i will filter the object what i can do it :

ex : 

```python
from django.shortcuts import render
from . models import product

# Create your views here.
# i will here not one and not all  i will filter how i will d

def product_list(request): 
    return render(request, 'products/product_list.html', {'product_list': product.objects.all( )filter()}) #-we have more method to do this 
# not foget that filter most with him loop make 

    


def product_detail(request):
    return render(request, 'products/product_detail.html')

```

----------------------------

## Django tutorial |  | query set exclude and order by and count objects :

ex : order 

```python
from django.shortcuts import render
from . models import product

# Create your views here.


def product_list(request):
    return render(request, 'products/product_list.html', {'product_list': product.objects.all().order_by('-price')})
#{'product_list': product.objects.all().order_by('name')})
# {'product_list': product.objects.all().order_by('content')})    


def product_detail(request):
    return render(request, 'products/product_detail.html')

```



ex : count 

here find we important  notice 

```python
from django.shortcuts import render
from . models import product

# Create your views here.


def product_list(request):
    return render(request, 'products/product_list.html', {'product_list': product.objects.all().count()}) # but we comme erorr because the result is integer and we need this to string 
#{'product_list':str( product.objects.all().count())})
    


def product_detail(request):
    return render(request, 'products/product_detail.html')

```



ex :  exclude (الاستثناء)  display all exclude ()

```python
from unicodedata import category
from django.shortcuts import render
from . models import product

# Create your views here.


def product_list(request):
    return render(request, 'products/product_list.html', {'product_list': (product.objects.all().exclude(category='Phone'))})
    


def product_detail(request):
    return render(request, 'products/product_detail.html')

```

not forget this method need to loop of the objects like this in the template 

```django
{% extends "base.html" %}




{% block content %}
{% for x in product_list %}
	<p>{{x.name}}</p>
	
	<p>{{x.content}}</p>
	
	<p>{{x.price}}</p>
	<hr>
	
{% endfor  %}


{% endblock content %}
```

-------------------

with 28
  

