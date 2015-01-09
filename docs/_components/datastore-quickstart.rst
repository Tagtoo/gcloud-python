Cloud Datastore in 10 seconds
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install the library
^^^^^^^^^^^^^^^^^^^

The source code for the library
(and demo code)
lives on GitHub,
You can install the library quickly with ``pip``::

  $ pip install gcloud

Run the demo
^^^^^^^^^^^^

In order to run the demo, you need to have registred an actual ``gcloud``
project and so you'll need to provide some environment variables to facilitate
authentication to your project:

  - ``GCLOUD_TESTS_PROJECT_ID``: Developers Console project ID (e.g.
    bamboo-shift-455).
  - ``GCLOUD_TESTS_DATASET_ID``: The name of the dataset your tests connect to.
    This is typically the same as ``GCLOUD_TESTS_PROJECT_ID``.
  - ``GCLOUD_TESTS_CLIENT_EMAIL``: The email for the service account you're
    authenticating with
  - ``GCLOUD_TESTS_KEY_FILE``: The path to an encrypted key file.
    See private key
    `docs <https://cloud.google.com/storage/docs/authentication#generating-a-private-key>`__
    for explanation on how to get a private key.

Run the
`example script <https://github.com/GoogleCloudPlatform/gcloud-python/blob/master/gcloud/datastore/demo/demo.py>`_
included in the package::

  $ python -m gcloud.datastore.demo

And that's it!
You just read and wrote a bunch of data
to the Cloud Datastore.

Try it yourself
^^^^^^^^^^^^^^^

You can interact with a demo dataset
in a Python interactive shell.

Start by importing the demo module
and instantiating the demo dataset::

  >>> from gcloud.datastore import demo
  >>> dataset = demo.get_dataset()

Once you have the dataset,
you can create entities and save them::

  >>> dataset.query('MyExampleKind').fetch()
  [<Entity{...}, ]
  >>> entity = dataset.entity('Person')
  >>> entity['name'] = 'Your name'
  >>> entity['age'] = 25
  >>> entity.save()
  >>> dataset.query('Person').fetch()
  [<Entity{...} {'name': 'Your name', 'age': 25}>]

.. note::
  The ``get_dataset`` method is just a shortcut for::

  >>> from gcloud import datastore
  >>> from gcloud.datastore import demo
  >>> dataset = datastore.get_dataset(
  >>>     demo.DATASET_ID, demo.CLIENT_EMAIL, demo.PRIVATE_KEY_PATH)

----
