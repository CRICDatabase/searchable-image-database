Contributor
===========

Code
----

Have a look at the source files
to see examples of how we structure things.

We use the following conventions based on [PEP8]_:

- Code should always use UTF-8
- Code should always use Unix line endings(``\n``)
- Use 4 spaces per indentation level
- Avoid trailing whitespace anywhere

Documentation
-------------

Have a look at the source files
to see examples of how we structure things.

We use the following conventions based on [RESTfulAPI.net]_ and [Tom2019]_:

- Format the JSON
- The endpoint shows the end path only
- Do not use trailing forward slash (/) in URIs
- Represent path parameters with curly braces, see `RFC 6570 <https://tools.ietf.org/html/rfc6570#section-2>`_
- Use realistic values in examples
- Format request examples in curl

Three Bash scripts are available to help with examples:

- ``docs/examples/run-all.sh`` will run all examples and update the output
- ``docs/examples/cric2localhost.sh`` change the domain in the examples from ``cricdatabase.com.br`` to ``localhost:3000``
- ``docs/examples/localhost2cric.sh`` change the domain in the examples from ``localhost:3000`` to ``cricdatabase.com.br``

..
    AuthorFirstName AuthorLastName. *Title of Article or Individual Page*. Title of website, Name of publisher, Date of publication, URL or DOI.

.. [PEP8] Guido van Rossum, Barry Warsaw, Nick Coghlan. *PEP 8 -- Style Guide
          for Python Code*. 2013. https://www.python.org/dev/peps/pep-0008/
.. [Tom2019] Tom Johnson. *Learn API Doc*. 2020. https://idratherbewriting.com/learnapidoc/.
.. [RESTfulAPI.net] RESTfulAPI.net. *REST Resource Naming Guide*. REST API Tutorial. 2020. https://restfulapi.net/resource-naming/.
