Getting Started
---------------

Installation
============

Install via pip:

.. code-block:: shell

    pip install django-sendfile2

And then add ``django_sendfile`` to ``INSTALLED_APPS`` in your settings module.

.. note::

    It is not strictly nessessary to have django_sendfile in
    ``INSTALLED_APPS``, but this may change in future.


You will need to have the following set in your settings module:

* ``SENDFILE_BACKEND`` - the dotted module notation of the backend you wish to use
* ``SENDFILE_ROOT`` - the directory you wish to serve files from

Additionally, you may wish to use the following optional settings:

* ``SENDFILE_CHECK_FILE_EXISTS`` - a bool defaulting to ``True``. When set to
  ``False`` backends that don't require direct file access will not produce a
  404 response if the file cannot be found locally.
* ``SENDFILE_URL`` - defines the internal URL prefix used by some backends. See
  the :doc:`backends` documentation for more details.


Use In Views
============

Use the :py:func:`~django_sendfile.sendfile` function instead of the usual
``HttpResponse`` function:

.. code-block:: python

    from django_sendfile import sendfile

    @login_required
    def my_secret_view(request):
        return sendfile(request, "/opt/my_secret.txt", mimetype="text/plain")

Alternatively, if you prefer class based views something like this would be required:

.. code-block:: python

    from django_sendfile import sendfile

    class MySecretView(LoginRequiredMixin, View):
        def render_to_response(self, context):
            return sendfile
