.. wrapper-label:

==========
C# Wrapper
==========

.. danger::

    Please make sure that you have read :ref:`Getting Started <getting-started-label>` because even the implementation is very different then default default *REST* approach, there are some concepts and issues described in much more details than it is here and some are assumed so there are no details at all.

The *C# Wrapper Library* that hides and abstracts the REST details under cover of wrapper and allows developers to use *REST API* in native way or in this case C# way. The *C# Wrapper Library* behind scene uses *JSON* as content media type.

The *C# Wrapper Library* also abstracts the authentication, *HTTP* ``PUT`` and ``DELETE`` verb issue in more easier way.

Setup and Dependencies
======================

Setup
~~~~~

To setup *C# Wrapper Library* there is a need to add the reference to ``Qualtrak.Coach.API.Wrappers.CSharp.dll`` provided with installation of *Coach*. Note that project framework is needed to be *.NET 4.5*, but note that *.NET 4.5 Client Profile* is not supported.

Dependencies
~~~~~~~~~~~~

The dependencis to run the *C# Wrapper Library* are:

* [JSON.NET](https://json.codeplex.com/releases) (actually the compiled name is ``Newtonsoft.Json.dll``).
* **CHECK OTHER DEPENDENCIES**

.. warning::

    The *C# Wrapper Library* uses Json.NET 4.5 Release 7 but any newer version should work properly.

Authentication
==============

Unlike send it in *HTTP Header* like in normal *REST* way this is abstract, but information is needed so it is a part of each C# Wrapper method. There is a need for providing the ``key`` and ``secret`` for each call to the *REST API*.

Response Content and API Wrapper
================================

Response Content is the data that is result of some request, and API wrapper is the way to send requests to *REST API*.

Response Content
~~~~~~~~~~~~~~~~

It is class ``ResponseContent`` that holds the *REST API* response message as its content.

Non-Generic Version
~~~~~~~~~~~~~~~~

The non-generic version of ``ResponseContet`` has two properties:

Error
-----

The ``Error`` property and it is an error response when some known error occurred due validation or some unknown exception occurred on server. The ``Error`` property  is actual Domain Model, read more in Client Errors

HttpStatusCode
--------------

The ``integer`` representation of *HTTP Staus Code* (eg. 200).

The Generic Version
~~~~~~~~~~~~~~~~~~~

The generic version ``ResponseContent<T>`` inherits from ``ResponseContent`` so it has its properties and also:

Result<T>
---------------

The ``Result<T>`` is a actual result data sent as response content, and the generic ``T`` can be List or Domain Model.

API Wrapper
~~~~~~~~~~~

The *API Wrapper* is actually interface ``IApiWrapper<TModel, TList>`` used is mostly all CRUD resources for *Coach Console API*.

The ``IApiWrapper<TModel, TList>`` has this methods:

ResponseContent<ICollection<TList>> GetAll()
--------------------------------------------------------

Method used for getting list of all request items that are collection of entity List Model.
The ``Result<T>`` will be sent if get all was successful if there is an error then the ``Error`` property will hold the error message.

ResponseContent<TModel> GetById(Guid id)
----------------------------------------------

Method used for getting a new or persisted instance of entity Domain Model. Use this method for getting default values on add and lookup data for both add and edit of entity.
The ``Result<T>`` will be sent if get by id was successful if there is an error then the ``Error`` property will hold the error message.

ResponseContent<TModel> Create(TModel entity)
----------------------------------------------

Method used for creating the resource. It expects created Domain Model to be sent and it returns this persisted Domain Model as it is called by ``GetById``.
The ``Result<T>`` will be sent if create was successful if there is an error then the ``Error`` property will hold the error message.

ResponseContent<TModel> Update(TModel entity, bool updateViaPost = false)
-------------------------------------------------------------------------

Method used for updating already persisted the resource. It expects updated Domain Model to be sent and it returns this updated Domain Model as it is called by ``GetById``.
The ``Result<T>`` will be sent if update was successful if there is an error then the ``Error`` property will hold the error message.

.. hint::

    The parameter ``updateViaPost`` is set by default to false and it will be using ``PUT`` on request, if this is issue, you can set it to ``true`` and will be using ``PUT`` via ``POST``.

ResponseContent Delete(Guid id, bool deleteViaPost = false)
-----------------------------------------------------------

Method used to delete resource by sending ``id``. It returns non-generic ``ResponseContent`` so there is no result just ``Error``. So if ``Error`` is not ``null`` then something went wrong on server.

.. hint::

    The parameter ``deleteViaPost`` is set by default to false and it will be using ``DELETE`` on request, if this is issue, you can set it to ``true`` and will be using ``DELETE`` via ``POST``.

.. warning::

    Note that all resources doesn't implement ``IApiWrapper<TModel, TList>`` like *Tenant*, *Tenant Tree* and *License*.
