.. _recorder-label:

========
Recorder
========

The **Recorder** is set of settings to integrate the media **Recorder** with *Coach* for playing media files and getting media files for *Evaluation*.

Recorder Components
===================

The **Recorder** components are: *Recorders*, *Media Players*, *Recorder Media Players*.

Recorders
^^^^^^^^^

A set of configuration settings that will connect **Recorder(s)** with *Coach*.

Media Players
^^^^^^^^^^^^^

Describes the way the media files will be played in *Coach*.

Recorder Media Players
^^^^^^^^^^^^^^^^^^^^^^

Here a **Recorder** that has been configured with *Coach* is combined with a **Media Player** that has been entered so that all media files evaluated in *Coach QM* from this **Recorder** will be replayed using this set **Media Player**.

Recorder Domain Model
=====================

Represent the **Recorder** domain model with available properties and its behaviors.

.. note::

  Note that domain model is used for write methods *POST* (*Create*) and *PUT* (*Update*) and as result of read-only method *GET/:id* (*GetById*).


+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| Name                                | Description                                                                                                      | Type                                   | Required  | Read-only                                      | Default               |
+=====================================+==================================================================================================================+========================================+===========+================================================+=======================+
| ``id``                              | Representing **Recorder** identifier.                                                                            | ``guid``                               | yes       | yes                                            |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``name``                            | The name of **Recorder**.                                                                                        | ``string(50)``                         | yes       | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``databaseServerIP``                | The **Recorder's** IP / domain name of SQL Server.                                                               | ``string(1000)``                       | no        | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``databaseName``                    | The **Recorder** database name that will be queried for media files.                                             | ``string(1000)``                       | no        | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``databaseUsername``                | The username of the DB login that will be used to gain access to the database.                                   | ``string(1000)``                       | no        | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``databasePassword``                | The password of the DB login that will be used to gain access to the database.                                   | ``string(1000)``                       | no        | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``databasePort``                    | The **Recorder's** database port.                                                                                | ``string(6)``                          | no        | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``serverIP``                        | The **Recorder** IP / domain name of where the database service is hosted.                                       | ``string(1000)``                       | yes       | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``tableName``                       | The **Recorder** DB table name where media files are persisted.                                                  | ``string(1000)``                       | yes       | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``communicationMethodType``         | The [communication method](/v1/recorder#communication-method) between *Coach* and the **Recorder**.              | ``byte``                               | yes       | no                                             | Direct Access ``1``   |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``databaseType``                    | The supported DB engines for getting **Recorder's** media files.                                                 | ``byte``                               | yes       | no                                             | SqlServer ``1``       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``searchCriteriaCollection``        | The **Recorder** collection of [Search Criteria](/v1/search-criteria).                                           | ``array(SearchCriteria)``              | no        | no                                             |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``mediaFileMetadataCollection``     | The **Recorder** [metadata for media files DB properties](/v1/media-metadata).                                   | ``array(MediaFileMetadata)``           | yes       | [partially](/v1/recorder#media-file-metadata)  |                       |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| **Lookups**                                                                                                                                                                                                                                                                          |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``communicationMethodTypes``        | The dictionary [Communication Method Types](/v1/recorder#communication-method) for ``communicationMethodType``.  |``dictionary(byte, string)``            | N/A       | N/A                                            | N/A                   |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``databaseTypes``                   | The dictionary of supported [Database Engine Types](/v1/player#database-type) for ``databaseType``.              | ``dictionary(byte, string)``           | N/A       | N/A                                            | N/A                   |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``databaseDataTypes``               | The dictionary of supported [Database Data Types](/v1/player) for ``databaseType``.                              | ``dictionary(byte, string)``           | N/A       | N/A                                            | N/A                   |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+
| ``searchDataTypesWithConditions``   | The collection of [Data Types and its supported Conditions](/v1/search-criteria#data-condition-model)            | ``array(SearchDataTypeWithCondition)`` | N/A       | N/A                                            | N/A                   |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------+----------------------------------------+-----------+------------------------------------------------+-----------------------+

.. note::

  The **Recorder** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Recorder** properties are capitalized (eg. ``Id``, ``Name``,..)!

.. danger::

  The *SQL Server* uses by default port 1433 and is not needed. If *MySQL* database is used the database port is required.

When the particular **Recorder** is acquired by *REST API*, for ``mediaFileMetadataCollection`` will be sent as collection of [supported/required media file metadata](/v1/media-metadata#supported-metadata). \\
Then there is only need for setting matching [Recorder's](/v1/recorder) ``fieldName`` and its [Database Data Type](/v1/media-metadata#database-data-types). \\
Note that the ``mediaFileMetadataCollection`` is read-only collection, collection items can only be changed, inserting or deleting items will result the exception from server.
{: #media-file-metadata .alert .alert-error .alert-block }


Communication Method Types
^^^^^^^^^^^^^^^^^^^^^^^^^^

Direct Access
-------------

.. warning::

  This options is being phased out

Direct connection to a **Recorder’s** database.

.. danger::

  Note that if *Direct Access* is chosen than properties ``databaseServerIP``, ``databaseName``, ``databaseUsername`` and ``databasePassword`` are required!


API
---

Connection to a **Recorder’s** repository when there is no direct connection available.

Database Types
^^^^^^^^^^^^^^

The *Coach* supported database engines for getting the **Recorder's** media files.

Currently the *Microsoft SQL Server* and *Oracle MySQL* database engines are supported.

Recorder List Model
===================

Represent the **Recorder** list  model with available properties.

.. note::

  | The list model used only to list **Recorders** with *GET* (*GetAll*) method.
  | Note that list model can change by adding/removing properties depending what recorders of *Coach REST API* will need in future.


+-------------------------------+-------------------------------------------------------------------------------+-------------+
| Name                          | Description                                                                   | Type        |
+===============================+=============================================================================================+
| ``id``                        | Representing **Recorder** identifier.                                         | ``guid``    |
+-------------------------------+-------------------------------------------------------------------------------+-------------+
| ``name``                      | The name of **Recorder**.                                                     | ``string``  |
+-------------------------------+-------------------------------------------------------------------------------+-------------+
| ``communicationMethodType``   | The **Recorder** communication method type.                                   | ``string``  |
+-------------------------------+-------------------------------------------------------------------------------+-------------+
| ``databaseType``              | The database engine type used for storing **Recorder** media files.           | ``string``  |
+-------------------------------+-------------------------------------------------------------------------------+-------------+
| ``serverIP``                  | The **Recorder** IP / domain name of where the database service is hosted.    | ``string``  |
+-------------------------------+-------------------------------------------------------------------------------+-------------+
| ``databaseServerIP``          | The **Recorder's** IP / domain name of SQL Server.                            | ``string``  |
+-------------------------------+-------------------------------------------------------------------------------+-------------+

.. note::

  The **Recorder** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Recorder** properties are capitalized (eg. ``Id``, ``Name``,..)!


List of Recorders
=================

The list of **Recorders** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/recorders

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in [Getting Started](/v1).


Return value
------------

* If there is no error: ``JSON`` array of [Recorder List Model](/v1/recorder#recorder-list-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderWrapper(int tenantCode, string apiKey, string apiSecret).GetAll();


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<ICollection<Recorder>>.Result`` object as collection of the [Recorder List Model](/v1/recorder#recorder-list-model).
* If there is an error: ``ResaultContent<ICollection<Recorder>>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   ITreeApiWrapper<Recorder, RecorderList> recorderWrapper = new RecorderWrapper(tenantCode, key, secret);
   ResponseContent<ICollection<RecorderList>> response = recorderWrapper.GetAll();

   if (response.Result != null)
   {
        // Use Result as List of Recorders for displaying.
        ICollection<RecorderList> recorders = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Get Recorder by Id
==================

The **Recorder** by requested Id for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/recorders/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Recorder** id, a valid and non-empty ``guid``.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in [Getting Started](/v1).


Return value
------------

* If there is no error: ``JSON`` as the [Recorder Domain Model](/v1/recorder#recorder-model) object.
* If there is an error: ``JSON`` as the :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderWrapper(int tenantCode, string apiKey, string apiSecret).GetById(Guid id);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Recorder** id, a valid and non-empty ``guid``.

Return value
------------

* If there is no error: ``ResaultContent<Recorder>.Result`` object as the [Recorder Domain Model](/v1/recorder#recorder-model).
* If there is an error: ``ResaultContent<Recorder>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid recorderId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   ITreeApiWrapper<Recorder, RecorderList> recorderWrapper = new RecorderWrapper(tenantCode, key, secret);
   ResponseContent<Recorder> response = recorderWrapper.GetById(recorderId);

   if (response.Result != null)
   {
        // Use Result as requested Recorder for displaying.
        Recorder recorder = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Create Recorder
===============

The creation of new **Recorder** for current :ref:`tenant-label`.

.. warning::

  To assign ``levels`` you'll need to get [Tenant Tree](/v1/tree) and use [Unit, Team or Agent](/v1/tree#levels-and-item-types) items as Levels!


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    POST /api/v1/:tenantCode/recorders

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``recorder`` ``JSON`` representation of [Recorder Domain Model](/v1/recorder#recorder-model) sent via *Request HTTP Header*.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in [Getting Started](/v1).


Return value
------------

* If there is no error: ``JSON`` representation of newly created **Recorder** as the [Recorder Domain Model](/v1/recorder#recorder-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderWrapper(int tenantCode, string apiKey, string apiSecret).Create(Recorder recorder);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``recorder`` The **Recorder** model constructed from **Recorder properties**.

Return value
------------

* If there is no error: ``ResaultContent<Recorder>.Result`` object as the [Recorder Domain Model](/v1/recorder#recorder-model).
* If there is an error: ``ResaultContent<Recorder>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   ITreeApiWrapper<Recorder, RecorderList> recorderWrapper = new RecorderWrapper(tenantCode, key, secret);
   // Get default data and lookup for recorder
   Recorder newRecorder = recorderWrapper.GetById(new Guid()).Result;
   newRecorder.Name = "Test Recorder with Direct Access";
   newRecorder.ServerIP = "localhost";
   newRecorder.DatabaseServerIP = "localhost";
   newRecorder.DatabaseName = "recordings";
   newRecorder.DatabaseUsername = "user";
   newRecorder.DatabasePassword = "$ecret";
   newRecorder.CommunicationMethodType = newRecorder.CommunicationMethodTypes
                                                    .Where(x => x.Value == "DirectAccess")
                                                    .Select(x => x.Key)
                                                    .SingleOrDefault();

   ResponseContent<Recorder> response = recorderWrapper.Create(newRecorder);

   if (response.Result != null)
   {
        // Use Result as newly created Recorder for display.
        Recorder recorder = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Update Recorder
===============

Updates already existent **Recorder** for current :ref:`tenant-label`.

.. warning::

  To assign ``levels`` you'll need to get [Tenant Tree](/v1/tree) and use [Unit, Team or Agent](/v1/tree#levels-and-item-types) items as Levels!


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    PUT /api/v1/:tenantCode/recorders/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Recorder** id, a valid and non-empty ``guid``.
* ``recorder`` ``JSON`` representation of [Recorder Domain Model](/v1/recorder#recorder-model) sent via *Request HTTP Header*.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in [Getting Started](/v1).
  | If you don't want to have in Web Server turned on the ``PUT`` verb method read more in [Getting Started](/v1).


Return value
------------

* If there is no error: ``JSON`` representation of uodated **Recorder** as the [Recorder Domain Model](/v1/recorder#recorder-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderWrapper(int tenantCode, string apiKey, string apiSecret).Update(Recorder recorder, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``recorder`` The **Recorder** model constructed from **Recorder properties** and ``Id`` must be provided in it. If not ``ArgumentException`` will be thrown!
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``PUT`` method. Default is ``false`` or use ``PUT`` method!

Return value
------------

* If there is no error: ``ResaultContent<Recorder>.Result`` object as the [Recorder Domain Model](/v1/recorder#recorder-model).
* If there is an error: ``ResaultContent<Recorder>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid recorderId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");


   ITreeApiWrapper<Recorder, RecorderList> recorderWrapper = new RecorderWrapper(tenantCode, key, secret);
   Recorder recorder = recorderWrapper.GetById(recorderId).Result;

   recorder.Name = "Test Recorder updated to API";
   recorder.ServerIP = "localhost";
   recorder.CommunicationMethodType = recorder.CommunicationMethodTypes
                                              .Where(x => x.Value == "API")
                                              .Select(x => x.Key)
                                              .SingleOrDefault();

   // Update via PUT method (default).
   ResponseContent<Recorder> response = recorderWrapper.Update(recorder);

   // Update via POST method (use true argument).
   // ResponseContent<Recorder> response = recorderWrapper.Update(recorder, true);

   if (response.Result != null)
   {
        // Use Result of updated Recorder for display.
        Recorder updatedRecorder = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Delete Recorder
===============

Deletes existent **Recorder** for current :ref:`tenant-label`.

.. warning::

  Note that **Recorder** will not be deleted if there are any references of **Recorder** in [Recorder Media Player](/v1/recorder-player).


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    DELETE /api/v1/:tenantCode/recorders/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Recorder** id, a valid and non-empty ``guid``.

.. danger::
  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in [Getting Started](/v1).
  | If you don't want to have in Web Server turned on the ``DELETE`` verb method read more in [Getting Started](/v1).


Return value
------------

* There is no return value except if there is an error, the ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderWrapper(int tenantCode, string apiKey, string apiSecret).Delete(Guid id, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Recorder** id, a valid and non-empty ``guid``.
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``DELETE`` method. Default is ``false`` or use ``DELETE`` method!

Return value
------------

* If there is no error: no return value or ``void``.
* If there is an error: ``ResaultContent<Recorder>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid recorderId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   ITreeApiWrapper<Recorder, RecorderList> recorderWrapper = new RecorderWrapper(tenantCode, key, secret);
   // Delete via DELETE method (default).
   ResponseContent response = recorderWrapper.Delete(recorderId);

   // DELETE via POST method (use true argument)..
   // ResponseContent response = recorderWrapper.Delete(recorderId, true);

   if (response.Error != null)
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
