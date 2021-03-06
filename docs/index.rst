sphinxcontrib-redoc
===================

.. hint::

    Check out `sphinxcontrib-openapi`_ if you are interested in rendering
    OpenAPI spec within Sphinx page (i.e. inline).

.. image:: _static/logo.png
   :width: 200
   :align: right

The Sphinx_ extension that renders OpenAPI_ (fka Swagger) specs with love
(❤️) using amazing ReDoc_. Don't believe it? Here's `the proof`_. Now stop
frustrating and start moving your projects to OpenAPI and ReDoc with this
small first step:

.. code:: bash

    $ pip install sphinxcontrib-redoc


Usage
-----

The whole configuration is done via Sphinx's ``conf.py``. All you have to
do is to:

* enable this extension

  .. code:: python

      extensions = [
         # ...
         'sphinxcontrib.redoc',
      ]

* define OpenAPI specs to render

  .. code:: python

      redoc = [
          {
              'name': 'Batcomputer API',
              'page': 'api',
              'spec': 'specs/batcomputer.yml',
          },
          {
              'name': 'Example API',
              'page': 'example/index',
              'spec': 'http://example.com/openapi.yml',
              'opts' {
                  'lazy': False,
                  'nowarnings': False,
                  'nohostname': False,
                  'required-props-first': True,
                  'expand-responses': [200, 201],
              }
          },
      ]

  where

  ``name``
    An API (human readable) name that will be used as page title.

  ``page``
    A page name to be used to form an output file. Passing ``api`` means:
    save rendered page as ``{outdir}/api.html``. It also support complex
    paths such as ``foo/bar/api`` which will be resolved into something
    like ``{outdir}/foo/bar/api.html``.

  ``spec``
    A path to an OpenAPI spec to be rendered. Can be either an HTTP(s)
    link to external source, or filesystem path relative to conf directory.

  ``opts``
    An optional dictionary with some of ReDoc settings that might be
    useful. Here they are

    ``lazy-rendering`` (default: ``False``)
      If set, enables lazy rendering mode which is useful for APIs with big
      number of operations (e.g. > 50). In this mode ReDoc shows initial
      screen ASAP and then renders the rest operations asynchronously while
      showing progress bar on the top.

    ``suppress-warnings`` (default: ``False``)
      If set, no warnings are rendered at the top of the document.

    ``hide-hostname`` (default: ``False``)
      If set, both protocol ans hostname are not shown in the operational
      definition.

    ``required-props-first`` (default: ``False``)
      If set, ReDoc shows required properties first in the same order as in
      ``required`` array. Please note, it may be slow.

    ``expand-responses`` (default: ``[]``)
      A list of response codes to be expanded by default.


Demo
----

* GitHub API

  * `the page <api/github/>`__
  * `the spec <_specs/github.yml>`__


Known Issues
------------

* ReDoc has some performance issues, so loading a pretty huge OpenAPI spec
  may take a time.


Changes
-------

.. include:: ../CHANGES.rst


Links
-----

* Documentation: https://sphinxcontrib-redoc.readthedocs.org/
* Source: https://github.com/ikalnytskyi/sphinxcontrib-redoc
* Bugs: https://github.com/ikalnytskyi/sphinxcontrib-redoc/issues


.. _Sphinx: https://www.sphinx-doc.org/
.. _OpenAPI: https://openapis.org/
.. _ReDoc: https://github.com/Rebilly/ReDoc
.. _the proof: api/github/
.. _sphinxcontrib-openapi: https://sphinxcontrib-openapi.readthedocs.io/
