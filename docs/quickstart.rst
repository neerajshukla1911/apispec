.. _quickstart:

Quickstart
==========

Basic Usage
-----------

First, create an `APISpec <apispec.APISpec>` object, passing basic information about your API.

.. code-block:: python

    from apispec import APISpec

    spec = APISpec(
        title='Gisty',
        version='1.0.0',
        info=dict(
            description='A minimal gist API'
        )
    )

Add definitions to your spec using `definition <apispec.APISpec.definition>`.

.. code-block:: python

    spec.definition('Gist', properties={
        'id': {'type': 'integer', 'format': 'int64'},
        'name': {'type': 'string'}
    })


Add paths to your spec using `add_path <apispec.APISpec.add_path>`.

.. code-block:: python


    spec.add_path(
        path='/gist/{gist_id}',
        operations=dict(
            get=dict(
                responses={
                    '200': {
                        'schema': {'$ref': '#/definitions/Gist'}
                    }
                }
            )
        )
    )

To output your OpenAPI spec, invoke the `to_dict <apispec.APISpec.to_dict>` method.

.. code-block:: python

    from pprint import pprint

    pprint(spec.to_dict())
    # {'definitions': {'Gist': {'properties': {'id': {'format': 'int64',
    #                                                 'type': 'integer'},
    #                                         'name': {'type': 'string'}}}},
    # 'info': {'description': 'A minimal gist API',
    #         'title': 'Gisty',
    #         'version': '1.0.0'},
    # 'parameters': {},
    # 'paths': {'/gist/{gist_id}': {'get': {'responses': {'200': {'schema': {'$ref': '#/definitions/Gist'}}}}}},
    # 'swagger': '2.0',
    # 'tags': []}

Use `to_yaml <apispec.APISpec.to_yaml>` to export your spec to YAML.

.. code-block:: python

    print(spec.to_yaml())
    # definitions:
    #   Pet:
    #     enum: [name, photoUrls]
    #     properties:
    #       id: {format: int64, type: integer}
    #       name: {example: doggie, type: string}
    # info: {description: 'This is a sample Petstore server.  You can find out more ', title: Swagger Petstore, version: 1.0.0}
    # parameters: {}
    # paths: {}
    # security:
    # - apiKey: []
    # swagger: '2.0'
    # tags: []

.. seealso::
    For a full reference of the `APISpec <apispec.APISpec>` class, see the :ref:`Core API Reference <core_api>`.


Next Steps
----------

We've learned how to programmatically construct an OpenAPI spec, but defining our entities was verbose.

In the next section, we'll learn how to let plugins do the dirty work: :ref:`Using Plugins <using_plugins>`
