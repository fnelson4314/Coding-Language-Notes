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
 
### Setting up a data model

- Creating database models is done with the class **from django.db import models**
- When creating the model class, it is done like:
  - **class Meeting(models.Model)**
    - **title = models.CharField(max_length=200)**
    - **date = models.DateField()**
- Run **python manage.py makemigrations** in order to look at our current model and create a migration in our migrations folder to prepare our table to be made
- Run **python manage.py migrate** in order to run the SQL and create the table
