MFRI Demo
=========

- Python 3
- Django 1.11
- Wagtail 1.11

systemd
-------

::

    sudo systemctl enable /srv/mfri-demo/systemd/mfri-demo.service 
    sudo systemctl start mfri-demo.service 

WhiteNoise
----------

(Via http://whitenoise.evans.io/en/stable/)

settings.py
~~~~~~~~~~~

::

    # Whitenoise
    BASE_DIR = os.path.dirname(os.path.abspath(__file__))
    STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
    STATICFILES_DIRS = (os.path.join(BASE_DIR, 'static'), )
    STATICFILES_STORAGE = 'whitenoise.django.GzipManifestStaticFilesStorage'
    MIDDLEWARE_CLASSES = [
      # 'django.middleware.security.SecurityMiddleware',
      'whitenoise.middleware.WhiteNoiseMiddleware',
      # ...
    ]

wsgi.py
~~~~~~~

::

    from whitenoise import WhiteNoise

    from my_project import MyWSGIApp

    application = MyWSGIApp()
    application = WhiteNoise(application, root='/path/to/static/files')
    application.add_files('/path/to/more/static/files', prefix='more-files/')

