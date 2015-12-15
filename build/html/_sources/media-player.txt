.. _media-player-label:

============
Media Player
============

**Media Player** describes the way the media files will be played in *Coach*.

Media Player Types
==================

Default Internal
^^^^^^^^^^^^^^^^

The Default Internal *Coach* Player is a Silverlight player and is to be used with those [Recorders](/v1/recorder) that use codecs compatible with Silverlight.

Custom Internal
^^^^^^^^^^^^^^^

The Custom Internal Player should be selected if you, the customer, will be using your own web-based player, or that of a third party, that meets a strict API compliance.

.. warning::

  The Internet Explorer browser uses Windows Media Player and Firefox / Chrome uses QuickTime.  It can be used any media player as long as it has an API that meets *Coach* playback contract. The player’s API must consist of the following API: Load (URL or ID), Play, Stop, Play, Seek from seconds, to seconds) and finally Get duration of recording in seconds. The player’s API must be accessible via javascript.

External
^^^^^^^^

This is when the player is contained in the user’s own application and *Coach* provides only recording playback details.

None
^^^^

*Coach* will provide no playback or playback details for recordings.


Media Player Domain Model
=========================

Represent the **Media Player** domain model with available properties and its behaviors.

.. note::

  Note that domain model is used for write methods *POST* (*Create*) and *PUT* (*Update*) and as result of read-only method *GET/:id* (*GetById*).


+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| Name               | Description                                                                                                     | Type                            | Required | Read-only | Default                   |
+====================+=================================================================================================================+=================================+==========+===========+===========================+
| ``id``             | Representing **Media Player** identifier.                                                                       | ``guid``                        | yes      | yes       |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``name``           | The name of **Media Player**.                                                                                   | ``string(50)``                  | yes      | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``type``           | The [type](/v1/player#media-player-types) of **Media Player**.                                                  | ``byte``                        | yes      | no        | Default internal (``1``)  |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``isAutoPlay``     | Denotes whether the media file will start instantly.                                                            | ``bool``                        | no       | no        | ``false``                 |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``publishingPoint``| The the name of the Windows Media Service publishing point of the root                                          | ``string(500)``                 | no       | no        |                           |
|                    | from where the media files are hosted. URL can be relative or absolute.                                         |                                 |          |           |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``playerUrl``      | URL of HTML file that contains the **Media Player**. URL can be relative or absolute.                           | ``string(500)``                 | no       | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``rootFolder``     |The URL of root folder from where the media files are hosted. URL can be relative or absolute.                   | ``string(500)``                 | no       | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``play``           | The Javascript function used to Play the media.                                                                 | ``string(50)``                  | no       | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``stop``           | The Javascript function used to Stop the media.                                                                 | ``string(50)``                  | no       | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``pause``          | The Javascript function used to Pause the media.                                                                | ``string(50)``                  | no       | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``seek``           | The Javascript function used to Seek the media.                                                                 | ``string(50)``                  | no       | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``load``           | The Javascript function used to Load the media.                                                                 | ``string(50)``                  | no       | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``length``         | The Javascript function used to return the length in seconds of the media.                                      | ``string(50)``                  | no       | no        |                           |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``lastSaved``      | The date the **Media Player** was last saved.                                                                   | ``datetime``                    | no       | no        | ``null``                  |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``loadType``       | The [load type](/v1/player#load-types) of **Media Player**.                                                     | ``byte``                        | no       | no        | None (``2``)              |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| **Lookups**                                                                                                                                                                                                               |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``types``          | The lookup dictionary of [Media Player Types](/v1/player#media-player-types). Used to set the ``playerType``.   | ``dictionary(byte, string)``    | N/A      | N/A       | N/A                       |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+
| ``loadTypes``      | The lookup dictionary of [Media Player Load Types](/v1/player#load-types). Used to set the ``loadType``.        | ``dictionary(byte, string)``    | N/A      | N/A       | N/A                       |
+--------------------+-----------------------------------------------------------------------------------------------------------------+---------------------------------+----------+-----------+---------------------------+

.. note::

  The **Media Player** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Media Player** properties are capitalized (eg. ``Id``, ``Name``,..)!


Media Player Required Properties By Player Type
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The table of required Domain Model properties depending on Media Player Type

+----------------------+---------------------+----------------+---------------+----------------+------------+------------+------------+------------+------------+------------+--------------+
| Player Type          | ``publishingPoint`` | ``isAutoPlay`` | ``playerUrl`` | ``rootFolder`` |  ``play``  |  ``stop``  |  ``pause`` |  ``stop``  |  ``seek``  | ``length`` | ``loadType`` |
+======================+=====================+================+===============+================+============+============+============+============+============+============+==============+
| **Default Internal** | ✔                   | ✔              |               |                |            |            |            |            |            |            |              |
+----------------------+---------------------+----------------+---------------+----------------+------------+------------+------------+------------+------------+------------+--------------+
| **Custom Internal**  |                     | ✔              | ✔             | ✔              | ✔          | ✔          | ✔          | ✔          | ✔          | ✔          | ✔            |
+----------------------+---------------------+----------------+---------------+----------------+------------+------------+------------+------------+------------+------------+--------------+
| **External**         |                     | N/A            |               |                |            |            |            |            |            |            |              |
+----------------------+---------------------+----------------+---------------+----------------+------------+------------+------------+------------+------------+------------+--------------+
| **None**             |                     | N/A            |               |                |            |            |            |            |            |            |              |
+----------------------+---------------------+----------------+---------------+----------------+------------+------------+------------+------------+------------+------------+--------------+

Media Player Load Types
^^^^^^^^^^^^^^^^^^^^^^^

It is the norm for a browser based player like WMP to accept an URL. However, in the cases where the media file has been encrypted, some propriety players insist on an ID. This ID will use to source the precise media file.

URL
---

Load URL into media player.

Id
--

Load ID into media player.

None
----

Do not load anything into media player.

Media Player List Model
=======================

Represent the **Media Player** list model with available properties.

.. note::

  | The list model used only to list **Media Players** with *GET* (*GetAll*) method.
  | Note that list model can change by adding/removing properties depending what users of *Coach REST API* will need in future.

+--------------------+-------------------------------------------------------------------+-------------+
| Name               | Description                                                       | Type        |
+====================+===================================================================+=============+
| ``id``             | Representing **Media Player** identifier.                         | ``guid``    |
+--------------------+-------------------------------------------------------------------+-------------+
| ``name``           | The name of **Media Player**.                                     | ``string``  |
+--------------------+-------------------------------------------------------------------+-------------+
| ``playerTypeName`` | The type of **Media Player**.                                     | ``string``  |
+--------------------+-------------------------------------------------------------------+-------------+
| ``lastSaves``      | The date when the **Media Player** was last saved.                | ``datetime``|
+--------------------+-------------------------------------------------------------------+-------------+

.. note::

  The **Media Player** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Media Player** properties are capitalized (eg. ``Id``, ``Name``,..)!


List of Media Players
=====================

The list of **Media Players** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/players

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` array of [Media Player List Model](/v1/player#media-player-list-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   MediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).GetAll();


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<ICollection<MediaPlayer>>.Result`` object collection of the [Media Player List Model](/v1/player#media-player-list-model).
* If there is an error: ``ResaultContent<ICollection<MediaPlayer>>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   ITreeApiWrapper<MediaPlayer, MediaPlayerList> mediaPlayerWrapper = new MediaPlayerWrapper(tenantCode, key, secret);
   ResponseContent<ICollection<MediaPlayerList>> response = mediaPlayerWrapper.GetAll();

   if (response.Result != null)
   {
        // Use Result as List of Media Players for displaying.
        ICollection<MediaPlayerList> mediaPlayers = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Get Media Player by Id
======================

The **Media Player** by requested Id for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/players/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Media Player** id, a valid and non-empty ``guid``.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` as the [Media Player Domain Model](/v1/player#media-player-model) object.
* If there is an error: ``JSON`` as the :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   MediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).GetById(Guid id);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Media Player** id, a valid and non-empty ``guid``.

Return value
------------

* If there is no error: ``ResaultContent<MediaPlayer>.Result`` object as the [Media Player Domain Model](/v1/player#media-player-model).
* If there is an error: ``ResaultContent<MediaPlayer>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid mediaPlayerId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   ITreeApiWrapper<MediaPlayer, MediaPlayerList> mediaPlayerWrapper = new MediaPlayerWrapper(tenantCode, key, secret);
   ResponseContent<MediaPlayer> response = mediaPlayerWrapper.GetById(mediaPlayerId);

   if (response.Result != null)
   {
        // Use Result as requested Media Player for displaying.
        MediaPlayer mediaPlayer = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Create Media Player
===================

The creation of new **Media Player** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    POST /api/v1/:tenantCode/players

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``mediaPlayer`` ``JSON`` representation of **Media Player properties** sent via *Request HTTP Header*.

.. danger::

  Remember to add *API Key* as *customer key* and *API Secret* as *customer secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of newly created **Media Player** as the [Media Player Domain Model](/v1/player#media-player-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   MediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).Create(MediaPlayer mediaPlayer);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``mediaPlayer`` The **Media Player** model constructed from **Media Player properties**.

Return value
------------

* If there is no error: ``ResaultContent<MediaPlayer>.Result`` object as the [Media Player Domain Model](/v1/player#media-player-model).
* If there is an error: ``ResaultContent<MediaPlayer>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   ITreeApiWrapper<MediaPlayer, MediaPlayerList> mediaPlayerWrapper = new MediaPlayerWrapper(tenantCode, key, secret);
   // Get default data and lookup for media players
   MediaPlayer newMediaPlayer = mediaPlayerWrapper.GetById(new Guid()).Result;
   newMediaPlayer.Name = "Media Player created from test";

   // Set type from media types lookup key.
   newMediaPlayer.Type = newMediaPlayer.Types.FirstOrDefault().Key;
   newMediaPlayer.PublishingPoint = "xyz";
   ResponseContent<MediaPlayer> response = mediaPlayerWrapper.Create(newMediaPlayer);

   if (response.Result != null)
   {
        // Use Result as newly created Media Player for display.
        MediaPlayer mediaPlayer = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }

Update Media Player
===================

Updates already existent **Media Player** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    PUT /api/v1/:tenantCode/players/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Media Player** id, a valid and non-empty ``guid``.
* ``mediaPlayer`` ``JSON`` representation of **Media Player properties** sent via *Request HTTP Header*.

.. danger::

  | Remember to add *API Key* as *customer key* and *API Secret* as *customer secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.
  | If you don't want to have in Web Server turned on the ``PUT`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of uodated **Media Player** as the [Media Player Domain Model](/v1/player#media-player-model) object.
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   MediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).Update(MediaPlayer mediaPlayer, bool updateViaPost = false);

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``mediaPlayer`` The **Media Player** model constructed from **Media Player properties** and ``Id`` must be provided in it. If not ``ArgumentException`` will be thrown!
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``PUT`` method. Default is ``false`` or use ``PUT`` method!

Return value
------------

* If there is no error: ``ResaultContent<MediaPlayer>.Result`` object as the [Media Player Domain Model](/v1/player#media-player-model).
* If there is an error: ``ResaultContent<MediaPlayer>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid mediaPlayerId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   ITreeApiWrapper<MediaPlayer, MediaPlayerList> mediaPlayerWrapper = new MediaPlayerWrapper(tenantCode, key, secret);
   MediaPlayer mediaPlayer = mediaPlayerWrapper.GetById(mediaPlayerId).Result;
   mediaPlayer.Name = "Media Player updated from test";
   mediaPlayer.PublishingPoint = "xyz updated";

   // Update via PUT method (default).
   ResponseContent<MediaPlayer> response = mediaPlayerWrapper.Update(mediaPlayer);

   // Update via POST method (use true argument).
   // ResponseContent<MediaPlayer> response = mediaPlayerWrapper.Update(mediaPlayer, true);

   if (response.Result != null)
   {
        // Use Result of updated Media Player for display.
        MediaPlayer updatedMediaPlayer = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Delete Media Player
===================

Deletes existent **Media Player** for current :ref:`tenant-label`.

.. warning::

  Note that **Media Player** will not be deleted if there are any references of **Media Player** in [Recorder Media Player](/v1/recorder-player).


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    DELETE /api/v1/:tenantCode/players/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Media Player** id, a valid and non-empty ``guid``.

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

   MediaPlayerWrapper(int tenantCode, string apiKey, string apiSecret).Delete(Guid id, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Media Player** id, a valid and non-empty ``guid``.
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``DELETE`` method. Default is ``false`` or use ``DELETE`` method!

Return value
------------

* If there is no error: no return value or ``void``.
* If there is an error: ``ResaultContent<MediaPlayer>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid mediaPlayerId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   ITreeApiWrapper<MediaPlayer, MediaPlayerList> mediaPlayerWrapper = new MediaPlayerWrapper(tenantCode, key, secret);
   // Delete via DELETE method (default).
   ResponseContent response = mediaPlayerWrapper.Delete(mediaPlayerId);

   // Delete via POST method (use true argument).
   // ResponseContent response = mediaPlayerWrapper.Delete(mediaPlayerId, true);

   if (response.Error != null)
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
