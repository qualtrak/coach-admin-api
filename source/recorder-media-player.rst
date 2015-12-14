.. _recorder-media-player-label:

=====================
Recorder Media Player
=====================

**Recorder Media Player** is combination of :ref:`recorder-label` and :ref:`media-player-label` that is used for :ref:`User (Agent) <user-label>` for getting recorded media file from :ref:`recorder-label` and playing it in way that is described in :ref:`media-player-label`.

Recorder Media Player Domain Model
==================================

Represent the **Recorder Media Player** domain model with available properties and its behaviors.

.. note::

  Note that domain model is used for write methods *POST* (*Create*) and *PUT* (*Update*) and as result of read-only method *GET/:id* (*GetById*).


+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+
| Name               | Description                                                                                             | Type                         | Required | Read-only | Default               |
+====================+=========================================================================================================+==============================+==========+===========+=======================+
| ``id``             | Representing **Recorder Media Player** identifier.                                                      | ``guid``                     | yes      | yes       |                       |
+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+
| ``name``           | The name of **Recorder Media Player**.                                                                  | ``string(255)``              | yes      | no        |                       |
+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+
| ``recorderId``     | The :ref:`recorder-label` reference.                                                                    | ``guid``                     | yes      | no        |                       |
+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+
| ``mediaPlayerId``  | The :ref:`media-player-label` reference.                                                                | ``guid``                     | yes      | no        |                       |
+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+
| ``isActive``       | Denotes whether the **Recorder Media Player** is active.                                                | ``bool``                     | yes      | no        | active (``true``)     |
+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+
| **Lookups**                                                                                                                                                                                                |
+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+
| ``recorders``      | The lookup dictionary of :ref:`recorder-label`. Used to set the ``redorderId``.                         | ``dictionary(guid, string)`` | N/A      | N/A       | N/A                   |
+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+
| ``mediaPlayers``   | The lookup dictionary of :ref:`Media Players <media-player-label>`. Used to set the ``mediaPlayerId``.  | ``dictionary(guid, string)`` | N/A      | N/A       | N/A                   |
+--------------------+---------------------------------------------------------------------------------------------------------+------------------------------+----------+-----------+-----------------------+

.. note::

  The **Recorder Media Player** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Recorder Media Player** properties are capitalized (eg. ``Id``, ``Name``,..)!

.. danger::

  | Note that only one unique combination of :ref:`recorder-label` and :ref:`media-player-label` can be set while creating/updating **Recorder Media Player**.
  | Matching same :ref:`recorder-label` and :ref:`media-player-label` twice will result as exception from server.


Recorder Media Player List Model
================================

Represent the **Recorder Media Player** list model with available properties.

.. note::

  | The list model used only to list **Media Players** with *GET* (*GetAll*) method.
  | Note that list model can change by adding/removing properties depending what users of *Coach REST API* will need in future.

+--------------------+----------------------------------------------------------------------------+-------------+
| Name               | Description                                                                | Type        |
+====================+============================================================================+=============+
| ``id``             | Representing **Recorder Media Player** identifier.                         | ``guid``    |
+--------------------+----------------------------------------------------------------------------+-------------+
| ``name``           | The name of **Recorder Media Player**.                                     | ``string``  |
+--------------------+----------------------------------------------------------------------------+-------------+
| ``isActive``       | Denotes whether the **Recorder Media Player** is active.                   | ``string``  |
+--------------------+----------------------------------------------------------------------------+-------------+
| ``recorderName``   | The name of :ref:`recorder-label`.                                         | ``string``  |
+--------------------+----------------------------------------------------------------------------+-------------+
| ``mediaPlayerName``| The name of :ref:`media-player-label`.                                     | ``string``  |
+--------------------+----------------------------------------------------------------------------+-------------+

.. note::

  The **Recorder Media Player** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Recorder Media Player** properties are capitalized (eg. ``Id``, ``Name``,..)!


List of Recorder Media Players
==============================

The list of **Recorder Media Players** for :ref:`Current Tenant <tenant-label>` .

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/recorder-players

Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` array of [Recorder Media Player List Model](/v1/recorder-player#recorder-player-list-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderMediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).GetAll();


Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`Current Tenant <tenant-label>` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`Current Tenant <tenant-label>` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<ICollection<RecorderMediaPlayer>>.Result`` object collection of the [Recorder Media Player List Model](/v1/recorder-player#recorder-player-list-model).
* If there is an error: ``ResaultContent<ICollection<RecorderMediaPlayer>>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   IApiWrapper<RecorderMediaPlayer, RecorderMediaPlayerList> recorderMediaPlayerWrapper = new RecorderMediaPlayerWrapper(tenantCode, key, secret);
   ResponseContent<ICollection<RecorderMediaPlayerList>> response = recorderMediaPlayerWrapper.GetAll();

   if (response.Result != null)
   {
        // Use Result as List of recorder Media Players for displaying.
        ICollection<RecorderMediaPlayerList> recorderMediaPlayers = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Get Recorder Media Player by Id
===============================

The **Recorder Media Player** by requested Id for :ref:`current Tenant <tenant-label>`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/recorder-players/:id

Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Recorder Media Player** id, a valid and non-empty ``guid``.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` as the [Recorder Media Player Domain Model](/v1/recorder-player#recorder-player-model) object.
* If there is an error: ``JSON`` as the :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderMediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).GetById(Guid id);


Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`Current Tenant <tenant-label>` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`Current Tenant <tenant-label>` API Secret provided by **Qualtrak**.
* ``id`` The **Recorder Media Player** id, a valid and non-empty ``guid``.

Return value
------------

* If there is no error: ``ResaultContent<RecorderMediaPlayer>.Result`` object as the [Recorder Media Player Domain Model](/v1/recorder-player#recorder-player-model).
* If there is an error: ``ResaultContent<RecorderMediaPlayer>.Error`` object. See more in :ref:`client-error-label`

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid recorderMediaPlayerId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper<RecorderMediaPlayer, RecorderMediaPlayerList> recorderMediaPlayerWrapper = new RecorderMediaPlayerWrapper(tenantCode, key, secret);
   ResponseContent<RecorderMediaPlayer> response = recorderMediaPlayerWrapper.GetById(recorderMediaPlayerId);

   if (response.Result != null)
   {
        // Use Result as requested Recorder Media Player for displaying.
        RecorderMediaPlayer recorderMediaPlayer = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Create Recorder Media Player
============================

The creation of new **Recorder Media Player** for :ref:`current Tenant <tenant-label>`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    POST /api/v1/:tenantCode/recorder-players

Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``recorderMediaPlayer`` ``JSON`` representation of **Recorder Media Player properties** sent via *Request HTTP Header*.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of newly created **Recorder Media Player** as the [Recorder Media Player Domain Model](/v1/recorder-player#recorder-player-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderMediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).Create(RecorderMediaPlayer recorderMediaPlayer);


Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`Current Tenant <tenant-label>` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`Current Tenant <tenant-label>` API Secret provided by **Qualtrak**.
* ``recorderMediaPlayer`` The **Recorder Media Player** model constructed from **Recorder Media Player properties**.

Return value
------------

* If there is no error: ``ResaultContent<RecorderMediaPlayer>.Result`` object as the [Recorder Media Player Domain Model](/v1/recorder-player#recorder-player-model).
* If there is an error: ``ResaultContent<recorderMediaPlayer>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   IApiWrapper<RecorderMediaPlayer, RecorderMediaPlayerList> recorderMediaPlayerWrapper = new RecorderMediaPlayerWrapper(tenantCode, key, secret);
   // Get default data and lookup for recorder media players
   RecorderMediaPlayer newRecorderMediaPlayer = recorderMediaPlayerWrapper.GetById(new Guid()).Result;
   newRecorderMediaPlayer.Name = "Recorder Media Player created from test";

   // Set recorder and mediaPlayer from lookups key.
   newRecorderMediaPlayer.RecorderId = newRecorderMediaPlayer.Recorders.FirstOrDefault().Key;
   newRecorderMediaPlayer.MediaPlayerId = newRecorderMediaPlayer.MediaPlayers.FirstOrDefault().Key;

   ResponseContent<RecorderMediaPlayer> response = recorderMediaPlayerWrapper.Create(newRecorderMediaPlayer);

   if (response.Result != null)
   {
        // Use Result as newly created Recorder Media Player for display.
        RecorderMediaPlayer recorderMediaPlayer = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Update Recorder Media Player
============================

Updates already existent **Recorder Media Player** for :ref:`current Tenant <tenant-label>` .

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    PUT /api/v1/:tenantCode/recorder-players/:id

Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Recorder Media Player** id, a valid and non-empty ``guid``.
* ``recorderMediaPlayer`` ``JSON`` representation of **recorder Media Player properties** sent via *Request HTTP Header*.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.
  | If you don't want to have in Web Server turned on the ``PUT`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of uodated **Recorder Media Player** as the [Recorder Media Player Domain Model](/v1/recorder-player#recorder-player-model) object.
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderMediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).Update(RecorderMediaPlayer recorderMediaPlayer, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`Current Tenant <tenant-label>` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`Current Tenant <tenant-label>` API Secret provided by **Qualtrak**.
* ``recorderMediaPlayer`` The **Recorder Media Player** model constructed from **Recorder Media Player properties** and ``Id`` must be provided in it. If not ``ArgumentException`` will be thrown!
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``PUT`` method. Default is ``false`` or use ``PUT`` method!

Return value
------------

* If there is no error: ``ResaultContent<RecorderMediaPlayer>.Result`` object as the [Recorder Media Player Domain Model](/v1/recorder-player#recorder-player-model).
* If there is an error: ``ResaultContent<RecorderMediaPlayer>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid recorderMediaPlayerId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper<RecorderMediaPlayer, RecorderMediaPlayerList> recorderMediaPlayerWrapper = new RecorderMediaPlayerWrapper(tenantCode, key, secret);
   RecorderMediaPlayer recorderMediaPlayer = recorderMediaPlayerWrapper.GetById(recorderMediaPlayerId).Result;
   recorderMediaPlayer.Name = "Recorder Media Player updated from test";
   recorderMediaPlayer.RecorderId = recorderMediaPlayer.Recorders.LastOrDefault().Key;
   recorderMediaPlayer.MediaPlayerId = recorderMediaPlayer.MediaPlayers.LastOrDefault().Key;

   // Update via PUT method (default).
   ResponseContent<RecorderMediaPlayer> response = recorderMediaPlayerWrapper.Update(recorderMediaPlayer);

   // Update via POST method (use true argument).
   // ResponseContent<RecorderMediaPlayer> response = recorderMediaPlayerWrapper.Update(recorderMediaPlayer, true);

   if (response.Result != null)
   {
        // Use Result of updated Recorder Media Player for display.
        RecorderMediaPlayer updatedRecorderMediaPlayer = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Delete Recorder Media Player
============================

Deletes existent **Recorder Media Player** for :ref:`current Tenant <tenant-label>` .

.. warning::

  Note that **Recorder Media Player** will not be deleted if there are any references of **Recorder Media Player** in [User](/v1/user).


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    DELETE /api/v1/:tenantCode/recorder-players/:id

Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Recorder Media Player** id, a valid and non-empty ``guid``.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.
  | If you don't want to have in Web Server turned on the ``DELETE`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* There is no return value except if there is an error, the ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   RecorderMediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).Delete(Guid id, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`Current Tenant <tenant-label>` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`Current Tenant <tenant-label>` API Secret provided by **Qualtrak**.
* ``id`` The **Recorder Media Player** id, a valid and non-empty ``guid``.
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``DELETE`` method. Default is ``false`` or use ``DELETE`` method!

Return value
------------

* If there is no error: no return value or ``void``.
* If there is an error: ``ResaultContent<RecorderMediaPlayer>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid recorderMediaPlayerId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper<RecorderMediaPlayer, RecorderMediaPlayerList> recorderMediaPlayerWrapper = new RecorderMediaPlayerWrapper(tenantCode, key, secret);
   // Delete via DELETE method (default).
   ResponseContent response = recorderMediaPlayerWrapper.Delete(recorderMediaPlayerId);

   // Delete via POST method (use true argument).
   // ResponseContent response = recorderMediaPlayerWrapper.Delete(recorderMediaPlayerId, true);

   if (response.Error != null)
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
