.. -*- mode: rst -*-

pymemcache-client
-----------------

Extension of Python package `pymemcache <https://pypi.python.org/pypi/pymemcache>`_ providing client configuration.


Badges
------

.. start-badges

.. list-table::
    :stub-columns: 1

    * - docs
      - |docs| |license|
    * - info
      - |hits| |contributors|
    * - tests
      - |travis| |coveralls|
    * - package
      - |version| |supported-versions|
    * - other
      - |requires|

.. |docs| image:: https://readthedocs.org/projects/pymemcache-client/badge/?style=flat
    :alt: Documentation Status
    :target: http://pymemcache-client.readthedocs.io

.. |hits| image:: http://hits.dwyl.io/TuneLab/pymemcache-client.svg
    :alt: Hits
    :target: http://hits.dwyl.io/TuneLab/pymemcache-client

.. |contributors| image:: https://img.shields.io/github/contributors/TuneLab/pymemcache-client.svg
    :alt: Contributors
    :target: https://github.com/TuneLab/pymemcache-client/graphs/contributors

.. |license| image:: https://img.shields.io/:license-apache-blue.svg
    :alt: License
    :target: https://opensource.org/licenses/Apache-2.0

.. |travis| image:: https://travis-ci.org/TuneLab/pymemcache-client.svg?branch=master
    :alt: Travis-CI Build Status
    :target: https://travis-ci.org/TuneLab/pymemcache-client

.. |coveralls| image:: https://coveralls.io/repos/TuneLab/pymemcache-client/badge.svg?branch=master&service=github
    :alt: Code Coverage Status
    :target: https://coveralls.io/r/TuneLab/pymemcache-client

.. |version| image:: https://img.shields.io/pypi/v/pymemcache-client.svg?style=flat
    :alt: PyPI Package latest release
    :target: https://pypi.python.org/pypi/pymemcache-client

.. |supported-versions| image:: https://img.shields.io/pypi/pyversions/pymemcache-client.svg?style=flat
    :alt: Supported versions
    :target: https://pypi.python.org/pypi/pymemcache-client

.. |requires| image:: https://requires.io/github/TuneLab/pymemcache-client/requirements.svg?branch=master
    :alt: Requirements Status
    :target: https://requires.io/github/TuneLab/pymemcache-client/requirements/?branch=master

.. end-badges


Install
-------

.. code-block:: bash

    pip install pymemcache-client


Install Memcached
-----------------

To run examples and tests locally upon **"localhost"**, memcached must be installed.

**Install memcached using brew**

.. code-block:: bash

    $ brew install memcached

    ==> Installing memcached
    ==> Downloading https://homebrew.bintray.com/bottles/memcached-1.5.3.sierra.bottle.tar.gz
    ######################################################################## 100.0%
    ==> Pouring memcached-1.5.3.sierra.bottle.tar.gz
    ==> Caveats
    To have launchd start memcached now and restart at login:
      brew services start memcached
    Or, if you don't want/need a background service you can just run:
      /usr/local/opt/memcached/bin/memcached
    ==> Summary
    🍺  /usr/local/Cellar/memcached/1.5.3: 11 files, 198.7KB


**Start memcached using brew**

.. code-block:: bash

    $ brew services start memcached

    ==> Successfully started `memcached` (label: homebrew.mxcl.memcached)

Architecture
------------

Extension of Python package `pymemcache <https://pypi.python.org/pypi/pymemcache>`_ returning ``from pymemcache.client.hash import HashClient``
and configured using either ``~/.pymemcache.json`` or ``pymemcache.json``.


Functionality
-------------

``class PymemcacheClient``: Prepare a Pymemcache Client using available configuration.

Configuration can be provided when creating an instance of this class by:

- User-level file: ``~/.pymemcache.json``
- Application-level file: ``./pymemcache.json``
- Provided as *file path* value in JSON-format to parameter ``config_file``
- Provided as ``dict`` value in JSON-format to parameter ``config``

Configuration
-------------

This is the expected configuration that can be provided to ``class PymemcacheClient`` is in JSON format:

.. code-block:: text

    {
        "client_type": "[OPTIONAL str, DEFAULT 'basic']",
        "servers": [
            {
                "host": "[str]",
                "port": [int]
            }
        ],
        "server_type": "[OPTIONAL str, DEFAULT 'standard']",
        "connect_timeout": [OPTIONAL float, Defaults to forever],
        "timeout": [OPTIONAL float, Defaults to forever],
        "no_delay": [OPTIONAL bool, DEFAULT false],
        "ignore_exc": [OPTIONAL bool, DEFAULT false],
        "default_noreply": [OPTIONAL bool, DEFAULT true],
        "allow_unicode_keys": [OPTIONAL bool, DEFAULT false]
    }

- ``"client_type"``: [OPTIONAL] Type of memcached client, DEFAULT ``"basic"``
    + ``"basic"``: Memcached client using ``from pymemcache.client.base import Client``. A client for a single memcached server.
    + ``"hash"``: Memcached client using ``from pymemcache.client.hash import HashClient``. A client for communicating with a cluster of memcached servers.
- ``"servers"``: A list of memcached servers and requiring at least one.
    + if ``"client_type"`` is ``"basic"``, then 1 server and only 1 is required.
    + if ``"client_type"`` is ``"hash"``, then 1 or more servers is required.
- ``"server_type"``: Defining special needs for connect to memcached servers, DEFAULT ``"standard"``.
    + ``"standard"``: Pooling server connections using standard HTTP.
    + ``"elasticache"``: Pooling server connections using Auto Discovery through `AWS Elasticache <http://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/AutoDiscovery.AddingToYourClientLibrary.html>`_.
- ``"connect_timeout"``: OPTIONAL float, seconds to wait for a connection to the memcached server. Defaults to "forever" (uses the underlying default socket timeout, which can be very long), i.e., the socket is put in blocking mode waiting to connect to memcached server.
- ``"timeout"``: OPTIONAL float, OPTIONAL float, seconds to wait for send or recv calls on the socket connected to memcached. Defaults to "forever" (uses the underlying default socket timeout, which can be very long), i.e., the socket is put in blocking mode.
- ``"no_delay"``: OPTIONAL bool, set the TCP_NODELAY flag, which may help with performance in some cases. DEFAULT ``false``.
- ``"ignore_exc"``: OPTIONAL bool, True to cause the "get", "gets", "get_many" and "gets_many" calls to treat any errors as cache misses. DEFAULT ``false``.
- ``"default_noreply"``: OPTIONAL bool, the DEFAULT value for ``'noreply'`` as passed to store commands. DEFAULT ``true``.
- ``"allow_unicode_keys"``: OPTIONAL bool, support unicode (utf8) keys. DEFAULT ``false``.


Dependencies
------------

``pymemcache-client`` module is built upon Python 3 and has dependencies upon
several Python modules available within `Python Package Index PyPI <https://pypi.python.org/pypi>`_.

- `pymemcache <https://pypi.python.org/pypi/pymemcache>`_
- `telnetlib3 <https://pypi.python.org/pypi/telnetlib3>`_
- `ujson <https://pypi.python.org/pypi/ujson>`_
