# Django

### Quick Important Terminal Commands

- **python manage.py runserver** starts the django server
- **python manage.py startapp appName** creates a package that will hold our new app
- **python manage.py makemigrations** looks at our current models and determines what changes we need to make to the database in order to match our model columns
- **python manage.py migrate** initializes our table and database

### Miscellaneous Notes
- **\<model>.objects.count()** - Every model/database has an "objects" attribute that can be called on


### Getting Started

- To start a django project, you can run **django-admin startproject \<projectName>**
- To run the django development server, run **python manage.py runserver**
  - Your webpage will be shown on the server that is generated after running
- To get the app started and actually get a view for it, run **python manage.py startapp appName**
  - This will create a new folder with your app name and inside it will have **views.py** which will be where the app visual content will be
  - After you add a new app, go to settings.py and add your new app name to the list of "INSTALLED_APPS"
- To add a new URL/new page, go to urls.py, and add to url patterns **path(urlAddition, function)**
  - Ex. **path('welcome.html', welcome)** and to see this, just add the urlAddition to the end of the url
    - **127.0.0.1:8000/welcome.html**
    - For the home page, just put in empty '' for the urlAddition
  - Might need to import as well, for example, **from website.views import welcome**
 
### Parts of the django project

- **admin.py** - Holds the content for providing admin access to a database
- **models.py** - Holds the content of all the models used for our databases
- **urls.py** - Holds all of the url additions and url paths that can be added to as you add more views
- **views.py** - Should contain all the code for rendering visual output to the website usually having functions that use templates
 
### Setting up a data model

- Creating database models is done with the class **from django.db import models**
- When creating the model class, it is done like:
```python
from datetime import time
from django.db import models

class Meeting(models.Model)
  title = models.CharField(max_length=200)
  date = models.DateField()
  start_time = models.TimeField(default=time(9))
  duration = models.IntegerField(default=1)
  room = models.ForeignKey(Room, on_delete=models.CASCADE) #Room is a separate class not shown and the cascade means that when a room is deleted, so will all meetings in that room

  #This method allows a nicer string representation to be shown in the admin interface
  def __str__(self):
    return f"{self.title} at {self.start_time} on {self.date}"
```
- Run **python manage.py makemigrations** in order to look at our current model and create a migration in our migrations folder to prepare our table to be made.
  - This will also be run whenever you made edits or editions to current models(Make sure you add defaults). It will create a new migration
- Run **python manage.py migrate** in order to run the SQL and create the table

### Admin interface

- This is normally already in your admin.py file, but **from django.contrib import admin** is needed at the top
- In admin.py, import the model you want to give admin privilages to **from .models import Meeting**
- Then you can add **admin.site.register(\<model>)**
- In order to login to the admin, you need to create a user account in terminal with **python manage.py createsuperuser**
- With this, you will be able to access and modify your table data

### Model, View, and Template

- Instead of the normal MVC pattern that other programs may follow, django uses an MVT pattern or model, view, and template
- Templates are basically incomplete html files waiting to be filled in by the programmer
- A "templates"(it should be named exactly like this) folder should be created inside your app folder where we will house our .html files
- In views, we can begin bringing in some template content to show on your website using **render** which renders a given template and returns an  HttpResponse object
```python
from django.shortcuts import render

def welcome(request):
  return render(request, "website/welcome.html") # The file path should be done relative to the "templates" folder
```

### Template variables and dynamic content

- To add onto the render method, more context can be added with the syntax **render(request, \<template>, \<Some dictionary for the template context>)**
```python
return render(request, "website/welcome.html", {"message": "This data was sent from the view to the template"})
```
- Variables inside the template can be called using double curly braces ({{     }})
  - **{{message}}**
- Loops are possible as well in the templates using {%   %}
```html
<ul>
  {% for meeting in meetings %}
    <li>
      <a href="{% url 'detail' meeting.id %}">
        {{meeting.title}}
      </a>
    </li>
  {% endfor %}
</ul>
```
- Doing this would require us to change our url path to **path('meetings/\<int:id>', detail, name="detail")** in order for the url template tag to find 'detail'

### Retrieving data from a database

- **\<model>.objects.\<method/attribute>** - Every model class has a .objects attribute that can be called on
- **.count()** can be used to get the total number of objects in the current database
- **.get()** can be used to retrieve a specific item from a database
  - Can add the argument **.get(pk=\<var>)** in order to specify the primary key you want to grab
  - Could also use the method **get_object_or_404(\<modelClass>, pk=id)** which either gets the object or returns a HTTP 404 not found error
    - Need to do **from django.shortcuts import get_object_or_404** to use
- **.all()** returns all objects in the database as a list
```python
def detail(request, id):
  meeting = Meeting.objects.get(pk=id)
  return render(request, "meetings/detail.html", {"meeting", meeting})
```
- This example id can be specified with a new url path in urls.py by doing **path('meetings/<int:id>, detail)**

### URLs and Link Building

- The **include()** method can be used to include urls from another file and simply add on to the current path
  - Let's say on the main url page we had **path('meetings/', include('meetings.urls'))**. This would append/include all the other url paths on the given file to the 'meetings/' url
  - Need to do **from django.urls import include** to use
 
### Styling

- You should add a "static" folder with another folder with the app name inside and this is where your CSS files will go
- In order to connect your style sheet to your templates, add **{% load static %}** at the top of your template file and add **\<link rel="stylesheet" href="{% static 'website/style.css' %}">**
- To add in an image, **\<img src="{% static 'wevsite/calendar.png' %}" width="100px">**

### Template Inheritance

Since many things in the template blocks are repeated, we should try to avoid this. To avoid it, we can have our parent file with all the repeated code
```html
{% load static %}
<!DOCTYPE>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{% block title %}{% endblock %}</title>
  <link rel="stylesheet" href="{% static 'website/style.css' %}">
</head>
<body>
  {% block content %}
  {% endblock %}
</body>
</html>
```

Then our child file with the filler code. title and content can be changed to different variables, but must be the same on the child files
```html
{% extends "base.html" %}

{% block title %}Meeting: {{meeting.title}}{% endblock %}

{% block content %}
<h1>{{meeting.title}}</h1>
<p>
  This meeting has been scheduled on {{meeting.date}}, at {{meeting.start_time}} in <strong>{{meeting.room}</strong>
</p>

<a href="{% url 'welcome' %}">Home</a>
{% endblock %}
```

### Template Composition

- {% include %} tags can be used to fully insert a template anywhere in your code.
- Let's say in the file "templates/footer.html", you have:
```html
<div>HOME | {{ me }} | ABOUT | FORUM | {{ sponsor }}</div>
```

Then in the file "templates/template.html", you have:
```html
<!DOCTYPE html>
<html>
<body>

{% include "mymenu.html" with me="TOBIAS" sponsor="W3SCHOOLS" %}

<h1>Welcome</h1>

<p>This is my webpage</p>

</body>
</html>
```

### User Interaction/Forms

In order to insert a form, you must first have a form tag for it to go in
```html
<form method="post">
  <table>
    {{ form }}
  </table>
  {% csrf_token %}
  <button type="submit">Create</button>
</form>
```
- Django already has something built in for forms
  - They can be accessed by importing **from django.forms import modelform_factory**
  - This can be captured using **MeetingForm = modelform_factory(<Model> exclude=[])**
 
Then to use this, do:
```html
def new(request):
  if request.method == "POST":
    form = MeetingForm(request.POST)
    if form.is_valid():
      form.save()
      return redirect("welcome")
  else:
    form = MeetingForm()
  return render(request, "meetings/new.html", {"form", form})
```

- The **redirect(\<url>)** method takes you to the specified page
  - Need to do **from django.shortcuts import redirect**
- The **.is_valid()** method checks to make sure the inputs are valid before saving to our database
- The "request" object has an attribute ".method" that let's us know if it is GET, POST, PUT, or DELETE
