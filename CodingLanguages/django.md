# Django

### Quick Important Commands

- **python manage.py runserver**
  - Starts the django server
- **python manage.py startapp appName**
  - Creates a package that will hold our new app
- **python manage.py makemigrations**
  - Looks at our current models and determines what changes we need to make to the database in order to match our model columns
- **python manage.py migrate**
  - Runs the SQL and our model to create a table 


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
- **views.py**
 
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


