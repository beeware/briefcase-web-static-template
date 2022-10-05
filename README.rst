Briefcase Static Web Template
=============================

A `Cookiecutter <https://github.com/cookiecutter/cookiecutter/>`__ template for
building Python apps that will run as statically-served web pages

Using this template
-------------------

The easiest way to use this project is to not use it at all - at least, not
directly. `Briefcase <https://github.com/beeware/briefcase/>`__ is a tool that
uses this template, rolling it out using data extracted from a
``pyproject.toml`` configuration file.

However, if you *do* want use this template directly...

1. Install `cookiecutter`_. This is a tool used to bootstrap complex project
   templates::

    $ pip install cookiecutter

2. Run ``cookiecutter`` on the template::

    $ cookiecutter https://github.com/beeware/briefcase-web-static-template

   This will ask you for a number of details of your application, including the
   `name` of your application (which should be a valid PyPI identifier), and
   the `Formal Name` of your application (the full name you use to describe
   your app). The remainder of these instructions will assume a `name` of
   ``my-project``, and a formal name of ``My Project``.

3. Build a wheel for your project, and add it to ``www/static/wheels``.

4. Add wheels for any additional project requirements to ``www/static/wheels``.

5. Add a file named ``www/pyscript.toml`` to configure the PyScript
   interpreter. At a minimum, it should include a ``packages`` declaration
   that includes all the wheels in the ``www/static/wheels`` folder.

If you've done this correctly, a project with a formal name of ``My Project``,
with an app name of ``my-project`` should have a directory structure that
looks something like::

    My Project/
        app/
            ...
        www/
            static/
                css/
                    briefcase.css
                wheels/
                    my_project-0.0.1-py3-none-any.whl
                    other-1.2.3-py3-none-any.whl
                favicon.png
            index.html
            pyscript.toml
        briefcase.toml

with ``www/pyscript.toml`` containing::

    packages = [
        "my_project-0.0.1-py3-none-any.whl",
        "other-1.2.3-py3-none-any.whl",
    ]

You should now be able to serve the `www` folder as a static website::

    $ python -m httpd.server --directory www

Next steps
----------

Of course, running Python code isn't very interesting by itself - you'll be
able to output to the web console, but that won't be visible to most users.

When the page loads, it will attempt to run ``my_project`` as a module (i.e.,
the equivalent of running ``python -m my_project`` from the command line).

To do something interesting, you'll need to add some DOM objects. You can use
`PyScript <https://pyscript.net>`__ APIs to manipulator the DOM.

Alternatively, you could use a cross-platform widget toolkit that supports the
web as a target (such as `Toga`_) to provide a GUI for your application.

.. _cookiecutter: https://github.com/cookiecutter/cookiecutter
.. _Toga: https://beeware.org/project/projects/libraries/toga
