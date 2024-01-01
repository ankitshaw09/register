# Django Authentication and Email Confirmation

This project demonstrates the implementation of Django's authentication system with email confirmation using crispy forms for enhanced form styling.

## Setup

1. Install required modules:

    ```bash
    pip install django django-crispy-forms
    ```

2. Create a Django project:

    ```bash
    django-admin startproject project
    cd project
    ```

3. Start the server:

    ```bash
    python manage.py runserver
    ```

4. Create a "user" app:

    ```bash
    python manage.py startapp user
    ```

5. Install crispy forms:

    ```bash
    pip install --upgrade django-crispy-forms
    ```

6. Update project settings (`settings.py`):

    ```python
    INSTALLED_APPS = [
        # ...
        'crispy_forms',
        'user',
    ]

    CRISPY_TEMPLATE_PACK = 'bootstrap4'
    ```

    Configure email settings:

    ```python
    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST = 'your_email_host'
    EMAIL_PORT = 587
    EMAIL_USE_TLS = True
    EMAIL_HOST_USER = 'your_email@gmail.com'
    EMAIL_HOST_PASSWORD = 'your_email_password'
    ```

7. Create URL patterns (`urls.py`):

    ```python
    # project/urls.py

    from django.contrib import admin
    from django.urls import path, include
    from user import views as user_views
    from django.contrib.auth import views as auth_views

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('user.urls')),
        path('login/', user_views.Login, name='login'),
        path('logout/', auth_views.LogoutView.as_view(template_name='user/index.html'), name='logout'),
        path('register/', user_views.register, name='register'),
    ]
    ```

    ```python
    # user/urls.py

    from django.urls import path
    from . import views

    urlpatterns = [
        path('', views.index, name='index'),
    ]
    ```

8. Create views (`views.py`):

    ```python
    # user/views.py

    # ... (previous imports)

    def index(request):
        return render(request, 'user/index.html', {'title': 'index'})

    def register(request):
        # ... (existing register function)

    def Login(request):
        # ... (existing login function)
    ```

9. Create forms (`forms.py`):

    ```python
    # user/forms.py

    from django import forms
    from django.contrib.auth.models import User
    from django.contrib.auth.forms import UserCreationForm

    class UserRegisterForm(UserCreationForm):
        # ... (existing UserRegisterForm)
    ```

10. Create templates:

    - `user/templates/user/index.html`
    - `user/templates/user/Email.html`
    - `user/templates/user/login.html`
    - `user/templates/user/register.html`

    (Refer to the provided HTML code for these templates.)

11. Make migrations and migrate:

    ```bash
    python manage.py makemigrations
    python manage.py migrate
    ```

12. Run the server:

    ```bash
    python manage.py runserver
    ```

Visit http://127.0.0.1:8000/ in your web browser to see the app in action.

## Conclusion

This Django project showcases a basic authentication system with email confirmation. Feel free to customize and enhance it based on your specific requirements.
