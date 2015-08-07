.. _getting-started-label:

===============
Getting Started
===============

Conventions used
=====

**Bold** - Mostly hyperlinks or just plain text for highlighting the current API page. Eg. in Tenant page there is no need to make link to itself it is just bold text.

*Italic* - Indicates highlighted words or meanings.

``id`` - Indicates the code properties and assigned values like true or null.

.. hint::

    Indicates some text that is a note to give more information on some subject.

.. warning::

    Indicate some text that warns of something that can happen and will not result in error.

.. danger::

    Indicate some text that will cause some errors and developers should be aware of its implication(s).

Coach
=====

The *Coach* has two main parts:

* *Console* the administrative part where the Tenant hierarchy can be created, connection to Recorder(s) and assign different Media Players for playback, and set Scheduled Tasks.
* *QM* or Quality Monitoring part for  media file monitoring standards to be established and then used to analytically evaluate files with the inclusion of carefully targeted coaching tools.

.. note::

    This *REST API* is fully implemented for administrative part of *Coach* or *Console* part. There are few settings that can be set for *QM* but they are all assigned through *Console API*.


Formats
=======

Currently supported format are *JSON* (JavaScript Object Notation) and *XML*. Requests are valid as long as they are sent as HTTP Header Content-Type *application/json* or *application/xml*, and result response format is same as sent request format.

Authentication
==============

With installation of *Coach* each customer will be provided with unique *API Key* and *API Secret*. The API `Key` and `Secret` are need for authentication to the *Coach REST API* and they are per Tenant base, so for each call to *REST API* service is used same combination of `Key` and `Secret`.

.. warning::

    It is up to developers using *Console REST API* to restrict or allow user to be able to gain access to *REST API*. From *REST API* point of view there is no distinction what user is using *REST API* since the same `Key` and `Secret` is used to gain access to the *Console API*.


A RESTful example
~~~~~~~~~~~~~~~~~

The *HTTP Header* is where you include the ``key`` and ``secret`` *fields*.  Please note the names of these *fields*; ``consumer_key`` and ``consumer_secret``:


.. code-block:: xml
   :linenos:

    consumer_key: neFh2vtr2sKH1tvsp0O6
    consumer_secret: 86h1qQEAhwlXydNJTLQj9KK3e5DUZUhoYjLsJKv72k44ZkmF2h


When issuing ``GET http://mydomain.com/aspire/api/v1/1001/users HTTP/1.1`` with the above *HTTP Header* the result will be *JSON* describing all the *Users* belonging to *Tenant* 1001

.. hint::

    The ``key`` and ``secret`` for the *Host Tenant* are created during the installation.  You can subsequently access and regenerate these values from within *Coach*.  Please refer to the *Coach Installation* documentation for further information.


Create, Update and Lookups
==========================

The *REST API* is constructed in a way that to create or update some resource it is needed to get resource by id that will populate the resource form with data, so it can be submitted to the server after changes made by user on form.

With get by id you'll get new or persisted instance of entity, with all default values already set (only on create) and also all the *lookup* (read more about about lookups in note below) data will be sent to client.

.. hint::

    The lookup in this sense is collection of ``key`` and ``value`` pairs needed to set some referenced id in some resource. It is used to populate drop boxes, radio buttons group,... The `key` of selected or checked item should be used to set some referenced value.

    Example would be to create *Team*, there is need to set it to a belonging *Unit* (``unitId``). The *Team* lookup ``units`` will provide you with all *Units* ``ids`` as ``key`` and *Unit* ``names`` as ``value`` of lookup so it is to set *Team's* belonging *Unit* by choosing one `key` and setting it to *Team's* ``unitId``.

The *lookup* enumeration keys are `integers` and `ids` used are `guids`.

To set up the form on adding/creating new entity is needed to use get by id and for ``id`` is needed to set and ``empty guid`` or ``"00000000-0000-0000-0000-000000000000"``, this will give you new instance of an entity with default values set and lookups for references loaded so that it can be use for form creation.

REST API Methods and Models
==============================

The API methods are the way to obtain data from *REST API* and models are way this data is represented.

Models
~~~~~~

The Models are representation of some resource as its properties and values assigned to it. The *Coach API* uses two kind of *Models*:

Domain Models
-------------

Used to for create and update domain model, but also for constructing and getting persisted **Domain Model**.

List Model
----------

The light and normalized version of **Domain Model** used for lists of resource (usually represented as grid or tabular data) and with fewer properties than **Domain Models** and instead of reference ``ids`` uses human readable ``name`` to show in list item.

.. hint::

    Note that **Domain Models** and **List Models** are described in lot more details about its properties and behaviors on each *API* resource page.

Methods
~~~~~~~

The *REST API* methods are analogous to *HTTP Verbs*. For most of resources in *REST API* you will have this five methods to get most common CRUD (Create Read Update Delete) data from and to server.

GET
---

Returns a list of all items for requested resource. It is sent as **List Model** and it is fully read-only data.
If there is error on server, it will send error response instead.

GET /:id
--------

Returns a **Domain Model** representation of resource for particular ``id``. Embedded with resources are *lookups*, and if is used ``empty guid`` it will already set all default values.
If there is error on server, it will send error response instead.

POST
----

Sends the newly created resource **Domain Model** and after saving it to database returns all the created values (now persisted) as it was called by ``GET :id``.
If there is error on server, it will send error response instead.

PUT
---

Sends the updated resource **Domain Model** and after saving it to database returns all the updated values (now persisted) as it was called by ``GET :id``.
If there is error on server, it will send error response instead.

DELETE
------

Sends the resources ``id`` to server to delete resource. After deletion if everything went well it will not send anything, but if there is error on server, error will be sent as response.

.. warning::

    Note that all resources don't have support for all methods described before.

    * The *Tenant* is currently supports only ``PUT`` or update (this will change with implementation of multi-tenancy).
    * The *Tenant Tree* is supports only ``GET`` method that or will bring only a Tenant Tree Items.
    * The *License* is now supports only ``GET`` method or will only obtain license from Licensing Server.



HTTP PUT and DELETE Issue
=========================

There are known issues with *HTTP* verbs ``PUT`` and ``DELETE``. The ``PUT`` and ``DELETE`` were not supported on older browsers and ``PUT`` and ``DELETE`` can be disabled or not disabled by default in *IIS Web Server*.

Activate PUT and DELETE on IIS Web Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To activate *HTTP* ``PUT`` and ``DELETE`` on *IIS Web Server* you need to add this part of configuration to the ``web.config`` of web application where *Coach REST API* is hosted.

.. hint::

    *Coach REST API* is hosted in same location as *Coach* Silverlight application is hosted.


For *IIS 7* and above you can use this configuration to enable ``PUT`` and ``DELETE``:

.. code-block:: xml
   :linenos:

       <system.webServer>
        <validation validateIntegratedModeConfiguration="false" />
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
          <add name="ExtensionlessUrlHandler-Integrated-4.0"
          path="*."
          verb="GET,HEAD,POST,DEBUG,PUT,DELETE"
          modules="IsapiModule"
          scriptProcessor="C:\Windows\Microsoft.NET\Framework64\v4.0.30319\aspnet_isapi.dll"
          resourceType="Unspecified"
          requireAccess="Script"
          preCondition="classicMode,runtimeVersionv4.0,bitness64"
          responseBufferLimit="0" />
        </handlers>
      </system.webServer>

.. warning::

    Please be aware that this piece of configuration is as-is, it is just example of enabling PUT and DELETE.
    For more information on enabling the PUT and DELETE in *IIS* please use *IIS* documentation or in house System Administrator if you have.

Using API with disabled PUT and DELETE
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Activating the *HTTP* ``PUT`` and ``DELETE`` is optional step, it is recommended, but optional. If from some case it is problem or it is in house rule to not allow ``PUT`` and ``DELETE`` or you still supporting browser that are not supporting this verbs then there is a way to sent *HTTP* ``PUT`` and ``DELETE`` as ``POST`` but with a *HTTP Header* directive ``X-HTTP-Method-Override``.

UPDATE via POST
~~~~~~~~~~~~~~~

To use ``UPDATE`` via ``POST`` you need to send ``POST`` request and in *HTTP Header* set:

.. code-block:: xml
   :linenos:

   X-HTTP-Method-Override: UPDATE

DELETE via POST
~~~~~~~~~~~~~~~

To use ``DELETE`` via ``POST`` you need to send ``POST`` request and in *HTTP Header* set:

.. code-block:: xml
   :linenos:

   X-HTTP-Method-Override: DELETE

TODO List
=========

* Finish Multi-Tenancy for Tenant via Create/Update/Delete + update documentation.
* Create Tenant Tree of only Unit/Team/Agent items for Schedule Level.
