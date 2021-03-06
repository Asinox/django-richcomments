Django Richcomments
===================
**Django app extending the builtin comments framework for AJAX style commenting.**

``django-richcomments`` wraps the Django's comments frameworks existing `render_comment_list <https://docs.djangoproject.com/en/dev/ref/contrib/comments/#std:templatetag-render_comment_list>`_ and `render_comment_form <https://docs.djangoproject.com/en/dev/ref/contrib/comments/#std:templatetag-render_comment_form>`_ template tags to make them behave AJAXy.

.. contents:: Contents
    :depth: 5

Installation
------------

#. Install or add ``django-richcomments`` to your Python path.

#. Configure Django's comments framework as described `here <https://docs.djangoproject.com/en/dev/ref/contrib/comments/#quick-start-guide>`_.

#. Add richcomments url include to your project's ``urls.py`` file::

    (r'^richcomments/', include('richcomments.urls')),

#. Ensure ``django-richcomments`` static media is accessible, see `managing static files <https://docs.djangoproject.com/en/dev/howto/static-files/>`_.

Usage
-----

``django-richcomments`` simply wraps the existing `render_comment_list <https://docs.djangoproject.com/en/dev/ref/contrib/comments/#std:templatetag-render_comment_list>`_ and `render_comment_form <https://docs.djangoproject.com/en/dev/ref/contrib/comments/#std:templatetag-render_comment_form>`_ template tags to make them behave AJAXy. Thus when a comment is submitted it is done via Javascript and an existing comment list is update without a page reload. You would customize your comment listing and form HTML as per normal. From a code perspective commenting behaves exactly the same as it normally does, except that the form generated by the ``render_comment_form`` tag will be submitted via AJAX and comment lists generated by the ``render_comment_list`` will be updated via AJAX after such a submit.

For richcomments to be active on a page both the `jQuery <http://jquery.com/>`_ and `jQuery form plugin <http://jquery.malsup.com/form/>`_ Javascript libraries needs to be loaded. Both are included as part of ``django-richcomments`` static media and a shortcut template tag is provided for your convenience, i.e.::
    
    {% load richcomments %}

    {% richcomments_static %}

which renders the following (with a static path as configured in your settings)::

    <script type="text/javascript" src="/static/richcomments/includes/jquery.min.js"></script>
    <script type="text/javascript" src="/static/richcomments/includes/jquery.form.js"></script>

To recap here's a simple example illustrating how you can display a list of comments as well as a comment form for an object which will be submitted and updated via AJAX::

    {% load comments richcomments %}

    <html>
        <head>
            {% richcomments_static %}
        </head>
        <body>
            {% render_comment_list for object %}
            {% render_comment_form for object %}
        </body>
    </html>


