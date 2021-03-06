Django-collage
==============

What's that
-----------
This reusable Django app can help you to create collages on your website
for gallery or another entities. For example, I'm use it for applications.

.. image:: https://raw.github.com/gotlium/django-collage/master/demo/screens/1.jpg
.. image:: https://raw.github.com/gotlium/django-collage/master/demo/screens/2.jpg
.. image:: https://raw.github.com/gotlium/django-collage/master/demo/screens/3.jpg
.. image:: https://raw.github.com/gotlium/django-collage/master/demo/screens/4.jpg
.. image:: https://raw.github.com/gotlium/django-collage/master/demo/screens/5.jpg
.. image:: https://raw.github.com/gotlium/django-collage/master/demo/screens/6.jpg
.. image:: https://raw.github.com/gotlium/django-collage/master/demo/screens/7.jpg


Installation:
-------------
1. Package:

.. code-block:: bash

    $ git clone https://github.com/gotlium/django-collage.git

    $ cd django-collage && sudo python setup.py install

**OR**

.. code-block:: bash

    $  sudo pip install django-collage

2. Add the ``collage`` application to ``INSTALLED_APPS`` in your settings file (usually ``settings.py``)
3. Sync database (``./manage.py syncdb``)


Usage:
------

models.py
~~~~~~~~~

.. code-block:: python

    class Entity(models.Model):
        name = models.CharField(max_length=255, unique=True)

        def get_images(self):
            return Images.objects.values_list('image', flat=True).filter(
                entity=self)


    class Images(models.Model):
        entity = models.ForeignKey(Entity)
        image = models.ImageField()


view.html
~~~~~~~~~
.. code-block:: html

    {% load collage %}
    {% load cache %}

    {% cache 31536000 images view.id %}
        {% get_collage for view.get_images as images %}
        <div>
          {% for image in images %}
            <a href="{{ image.src }}" style="{{ image.css }}">
              <img src="{{ image.url }}">
            </a>
          {% endfor %}
        </div>
    {% endcache %}


.. image:: https://d2weczhvl823v0.cloudfront.net/gotlium/django-collage/trend.png
   :alt: Bitdeli badge
   :target: https://bitdeli.com/free

