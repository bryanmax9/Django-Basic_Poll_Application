<img src="https://i.imgur.com/CEMykWV.png" alt="MLH-banner" width="100%" height="400px">

# Django-Basic_Poll_Application - Learn to Create a Django Project! 👻

 
<h3>🐧 I am creating this step-by-step Basic Django Project for anyone interested in Learning this Framework!</h3>

# ⭐ Step 1:

Make sure to Download First Django on your computer, here is the link to Download Django from its official Website using the instructions provided: https://www.djangoproject.com/

Make sure you successfully installed Django using the following command:
   ```bash
   python -m django --version
   ```

# ⭐ Step 2:
<h3>Creating a project</h3>
From the command line, cd into a directory where you’d like to store your code, then run the following command:

* For MAC/Linux
   ```bash
   python3 -m django startproject mysite
   ```

* For Windows
  ```bash
  python -m django startproject mysite
  ```

This will create a mysite directory in your current directory. If it didn’t work, see <a href="https://docs.djangoproject.com/en/4.0/faq/troubleshooting/#troubleshooting-django-admin" >Problems running django-admin</a>.

Let’s look at what startproject created:

  ```bash
  mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
  ```
These files are:

* The outer mysite/ root directory is a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.
* manage.py: A command-line utility that lets you interact with this Django project in various ways. You can read all the details about manage.py in <a href="https://docs.djangoproject.com/en/4.0/ref/django-admin/">django-admin and manage.py</a>.
* The inner mysite/ directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. mysite.urls).
* mysite/__init__.py: An empty file that tells Python that this directory should be considered a Python package. If you’re a Python beginner, read <a href="https://docs.python.org/3/tutorial/modules.html#tut-packages">more about packages</a> in the official Python docs.
* mysite/settings.py: Settings/configuration for this Django project. <a href="https://docs.djangoproject.com/en/4.0/topics/settings/">Django settings</a> will tell you all about how settings work.
* mysite/urls.py: The URL declarations for this Django project; a “table of contents” of your Django-powered site. You can read more about URLs in <a href="https://docs.djangoproject.com/en/4.0/topics/http/urls/">URL dispatcher</a>.
* mysite/asgi.py: An entry-point for ASGI-compatible web servers to serve your project. See <a href="https://docs.djangoproject.com/en/4.0/howto/deployment/asgi/">How to deploy with ASGI</a> for more details.
* mysite/wsgi.py: An entry-point for WSGI-compatible web servers to serve your project. See <a href="https://docs.djangoproject.com/en/4.0/howto/deployment/wsgi/">How to deploy with WSGI</a> for more details.

# ⭐ Step 3:
<h3>The development server</h3>
Let’s verify your Django project works. cd into mysite directory, if you haven’t already, and run the following commands:

* For MAC/Linux
   ```bash
   python manage.py runserver
   ```

* For Windows
  ```bash
  py manage.py runserver
  ```

You’ll see the following output on the command line:

  ```bash
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

February 14, 2023 - 15:50:53
Django version 4.0, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
  ```

🚀  You’ve started the Django development server, a lightweight web server written purely in Python. We’ve included this with Django so you can develop things rapidly, without having to deal with configuring a production server – such as Apache – until you’re ready for production.

Now’s a good time to note: don’t use this server in anything resembling a production environment. It’s intended only for use while developing. (We’re in the business of making web frameworks, not web servers.)

Now that the server’s running, visit http://127.0.0.1:8000/ with your web browser. You’ll see a “Congratulations!” page, with a rocket taking off. It worked! 🚀

# ⭐ Step 4:
<h3>Creating the Polls app</h3>
🧑‍💻Now that your environment is set up, you’re set to start doing work.



<strong >Each application you write in Django consists of a Python package that follows a certain convention. Django comes with a utility that automatically generates the basic directory structure of an app, so you can focus on writing code rather than creating directories.</strong>



Your apps can live anywhere on your Python path. In this tutorial, we’ll create our poll app in the same directory as your manage.py file so that it can be imported as its own top-level module, rather than a submodule of mysite.

To create your app, make sure you’re in the same directory as manage.py and type this command:

* For MAC/Linux
   ```bash
   python manage.py startapp polls
   ```

* For Windows
  ```bash
  py manage.py startapp polls
  ```


That’ll create a directory polls, which is laid out like this:
```bash
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

This directory structure will house the poll application. 😎


# ⭐ Step 5:
<h3>Write your first view</h3>
Let’s write the first view. Open the file "polls/views.py" and put the following Python code in it:

```bash
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

This is the simplest view possible in Django. To call the view, we need to map it to a URL - and for this, we need a URLconf.

To create a URLconf in the polls directory, create a file called urls.py. Your app directory should now look like:

```bash
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    urls.py
    views.py
```

In the polls/urls.py file include the following code:
```bash
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

The next step is to point the root URLconf at the polls.urls module. In mysite/urls.py, add an import for django.urls.include and insert an include() in the urlpatterns list, so you have:

```bash
from django.contrib import admin
from django.urls import include path
from django.views.generic import RedirectView # for redirecting polls/ to be redirected to root URL

urlpatterns = [
    path('', RedirectView.as_view(url='/polls/')), # Redirect root URL to /polls/ on page load.
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]


```

The include() function in Django is used to link to another set of URL configurations. When Django sees include(), it removes the matched part of the URL and uses the rest of the URL to find views based on the linked URL configurations.

In simpler terms, include() lets you organize and reuse URL patterns. For example, if you have URL patterns for a polls app in polls/urls.py, you can use them under different paths like “/polls/”, “/fun_polls/”, or “/content/polls/”, without changing the app itself.

For example, if you want to use paths like "/content/polls/" , you would modify the URL patterns list to include those paths. 

For "/content/polls/":
```bash
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('content/polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]

```



# ⭐ Step 5 - Finall Step 🥳:
<h3>You have now wired an index view into the URLconf.</h3>

Verify it’s working with the following command:

* For MAC/Linux
   ```bash
   python manage.py runserver
   ```

* For Windows
  ```bash
  py manage.py runserver
  ```
Go to http://localhost:8000/polls/ in your browser, and you should see the text “Hello, world. You’re at the polls index.”, which you defined in the index view.


## Congratulations! You just Created your first Basic Django App 😎🐧🥳🚀👻

# Sources used to create this Tutorial Possible 🌍
https://docs.djangoproject.com/en/4.0/intro/tutorial01/
