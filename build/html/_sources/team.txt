.. _team-label:

====
Team
====

A **Team** is the ‘end point’ to a branch of your organization and it is the only element of an organization that can have *Agents* assigned to it.

.. note::

  A **Team** can only be added to a :ref:`unit-label` or a sub-Unit. \\
  A **Team** cannot be added to a reversibly deleted and/or inactive :ref:`unit-label` or sub-Unit.


Team Domain Model
=================

Represent the **Team** domain model with available properties and its behaviors.

.. note::

  Note that domain model is used for write methods *POST* (*Create*) and *PUT* (*Update*) and as result of read-only method *GET/:id* (*GetById*).


+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| Name               | Description                                                            | Type                         | Required | Read-only   | Default                 |
+====================+========================================================================+==============================+==========+=============+=========================+
| ``id``             | Representing **Team** identifier.                                      | ``guid``                     | yes      | yes         |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``name``           | The name of **Team**.                                                  | ``string(50)``               | yes      | no          |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``description``    | The description of **Team**.                                           | ``string(50)``               | no       | no          |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``isActive``       | Denotes whether the **Team** state is active or inactive.              | ``boolean``                  | yes      | no          | active (``true``)       |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``isDeleted``      | Denotes whether the **Team** state is deleted or not.                  | ``boolean``                  | yes      | [partially] | not deleted (``false``) |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``unitId``         | Represent the belonging :ref:`unit-label`.                             | ``guid``                     | yes      | no          |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``showScore``      | Displays percentage score in *QM Evaluation* while is being            | ``boolean``                  | yes      | no          | don't show (``false``)  |
|                    | created instead of default when *Evaluation* is completed.             |                              |          |             |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``managers``       | The **Team** assigned [Managers (User)](/v1/user).                     | ``array(guid)``              | no       | no          |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``members``        | The **Team** assigned [Members (User)](/v1/user).                      | ``array(guid)``              | no       | no          |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| **Lookups**                                                                                                                                                                   |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``unitsLookup``    | The lookup dictionary of active and not deleted :ref:`unit-label`,     | ``dictionary(guid, string)`` | N/A      | N/A         | N/A                     |
|                    | needed for choosing belonging :ref:`unit-label` and setting ``unitId`` |                              |          |             |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+
| ``usersLookup``    | The dictionary of active and not deleted [Users](/v1/user),            | ``dictionary(guid, string)`` | N/A      | N/A         | N/A                     |
|                    | needed for setting the **Team** ``managers`` and ``members``.          |                              |          |             |                         |
+--------------------+------------------------------------------------------------------------+------------------------------+----------+-------------+-------------------------+

.. note::

  The **Team** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Team** properties are capitalized (eg. ``Id``, ``Name``,..)!

.. warning::

  | **Active and Deleted Logic**
  |
  | When **Team** is deleted by [Delete command](/v1/team#team-delete) and it is flagged as ``isDeleted`` as ``true`` and also by default it is flagged ``isActive`` as ``false``. Note that  status ``isActive`` will remain "*locked*" until the **Team's** ``isDeleted`` state is updated to ``false`` or *not deleted* anymore. Then ``isActive`` is "*unlocked*" and can be changed. If the **Team** is *deleted* and on update is tried to change ``isActive`` property, server will silently ignore sent ``isActive`` property.
  |
  | [Team Manager(s)](/v1/user), [Team Agent(s)](/v1/user) and [belonging Unit](/v1/unit) can be set to only *active* and *not deleted* **Teams**. If is sent otherwise to *inactive* and/or *deleted* **Team**, server will silently ignore those assignments.


Team List Model
===============

Represent the **Team** list model with available properties.

.. note::

  | The list model used only to list **Teams** with *GET* (*GetAll*) method.
  | Note that list model can change by adding/removing properties depending what users of *Coach REST API* will need in future.


+-----------------+-----------------------------------------------------------+-------------+
| Name            | Description                                               | Type        |
+=================+===========================================================+=============+
| ``id``          | Representing **Team** identifier.                         | ``guid``    |
+-----------------+-----------------------------------------------------------+-------------+
| ``name``        | The name of **Team**.                                     | ``string``  |
+-----------------+-----------------------------------------------------------+-------------+
| ``description`` | The description of **Team**.                              | ``string``  |
+-----------------+-----------------------------------------------------------+-------------+
| ``isActive``    | Denotes whether the **Team** state is active or inactive. | ``boolean`` |
+-----------------+-----------------------------------------------------------+-------------+
| ``isDeleted``   | Denotes whether the **Team** state is deleted or not.     | ``boolean`` |
+-----------------+-----------------------------------------------------------+-------------+
| ``unitName``    | The name of belonging :ref:`unit-label`. Needed           | ``string``  |
|                 | for representing the parent unit in list of Team.         |             |
+-----------------+-----------------------------------------------------------+-------------+

.. note::

  The **Team** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Team** properties are capitalized (eg. ``Id``, ``Name``,..)!


List of Teams
=============

The list of **Teams** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/teams

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` array of [Team List Model](/v1/team#team-list-model).
* If there is an error: ``JSON`` [error](/v1/client-errors#error-model) object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   TeamWrapper(int tenantCode, string apiKey, string apiSecret).GetAll();


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<ICollection<Team>>.Result`` object collection of the [Team List Model](/v1/team#team-list-model).
* If there is an error: ``ResaultContent<ICollection<Team>>.Error`` object. See more in [Client Errors](/v1/client-errors).

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   IApiWrapper&lt;Team, TeamList&gt; teamWrapper = new TeamWrapper(tenantCode, key, secret);
   ResponseContent&lt;ICollection&lt;TeamList&gt;&gt; response = teamWrapper.GetAll();

   if (response.Result != null)
   {
        // Use Result as List of Teams for displaying.
        ICollection&lt;TeamList&gt; teams = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Get Team by Id
==============

The **Team** by requested Id for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/teams/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Team** id, a valid and non-empty ``guid``.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` as the [Team Domain Model](/v1/team#team-model) object.
* If there is an error: ``JSON`` as the [error](/v1/client-errors#error-model) object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   TeamWrapper(int tenantCode, string apiKey, string apiSecret).GetById(Guid id);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Team** id, a valid and non-empty ``guid``.

Return value
------------

* If there is no error: ``ResaultContent<Team>.Result`` object as the [Team Domain Model](/v1/team#team-model).
* If there is an error: ``ResaultContent<Team>.Error`` object. See more in [Client Errors](/v1/client-errors).

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid teamId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper&lt;Team, TeamList&gt; teamWrapper = new TeamWrapper(tenantCode, key, secret);
   ResponseContent&lt;Team&gt; response = teamWrapper.GetById(teamId);

   if (response.Result != null)
   {
        // Use Result as requested Team for displaying.
        Team team = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Create Team
===========

The creation of new **Team** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    POST /api/v1/:tenantCode/teams

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``team`` ``JSON`` representation of **Team properties** sent via *Request HTTP Header*.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of newly created **Team** as the [Team Domain Model](/v1/team#team-model).
* If there is an error: ``JSON`` [error](/v1/client-errors#error-model) object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   TeamWrapper(int tenantCode, string apiKey, string apiSecret).Create(Team team);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``team`` The **Team** model constructed from **Team properties**.

Return value
------------

* If there is no error: ``ResaultContent<Team>.Result`` object as the [Team Domain Model](/v1/team#team-model).
* If there is an error: ``ResaultContent<Team>.Error`` object. See more in [Client Errors](/v1/client-errors).

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   IApiWrapper&lt;Team, TeamList&gt; teamWrapper = new TeamWrapper(tenantCode, key, secret);
   // Get default data and lookup for teams
   Team newTeam = teamWrapper.GetById(new Guid()).Result;
   newTeam.Name = "Team created from test";
   newTeam.Description = "Team created from test description.";
   // Set belonging Unit key from units lookup key.
   newTeam.UnitId = newTeam.Units.FirstOrDefault().Key;
   ResponseContent&lt;Team&gt; response = teamWrapper.Create(newTeam);

   if (response.Result != null)
   {
        // Use Result as newly created Team for display.
        Team team = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Update Team
===========

Updates already existent **Team** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    PUT /api/v1/:tenantCode/teams/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Team** id, a valid and non-empty ``guid``.
* ``team`` ``JSON`` representation of **Team properties** sent via *Request HTTP Header*.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`. \\
  | If you don't want to have in Web Server turned on the ``PUT`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of uodated **Team** as the [Team Domain Model](/v1/team#team-model) object.
* If there is an error: ``JSON`` [error](/v1/client-errors#error-model) object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   TeamWrapper(int tenantCode, string apiKey, string apiSecret).Update(Team team, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``team`` The **Team** model constructed from **Team properties** and ``Id`` must be provided in it. If not ``ArgumentException`` will be thrown!
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``PUT`` method. Default is ``false`` or use ``PUT`` method!

Return value
------------

* If there is no error: ``ResaultContent<Team>.Result`` object as the [Team Domain Model](/v1/team#team-model).
* If there is an error: ``ResaultContent<Team>.Error`` object. See more in [Client Errors](/v1/client-errors).

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid teamId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper&lt;Team, TeamList&gt; teamWrapper = new TeamWrapper(tenantCode, key, secret);
   Team team = teamWrapper.GetById(teamId).Result;
   team.Name = "Team updated from test";
   team.Description = "Team updated from test description.";
   // Set belonging Unit key from units lookup key.
   team.UnitId = team.Units.FirstOrDefault().Key;

   // Update via PUT method (default).
   ResponseContent&lt;Team&gt; response = teamWrapper.Update(team);

   // Update via POST method (use true argument).
   // ResponseContent&lt;Team&gt; response = teamWrapper.Update(team, true);

   if (response.Result != null)
   {
        // Use Result of updated Team for display.
        Team updatedTeam = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Delete Team
===========

Deletes existent **Team** for current :ref:`tenant-label`.

.. warning::

  | Note that if **Team** has assigned *Team Managers* and *Agents* then **Team** will not be deleted but flagged as ``isDeleted``. When **Team** is deleted it can be undeleted by setting ``isDeleted`` to ``false`` while updating **Team**. \\
  | If **Team** has no assigned *Team Managers* and *Agents*, it will be deleted permanently.


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    DELETE /api/v1/:tenantCode/teams/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Team** id, a valid and non-empty ``guid``.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`. \\
  | If you don't want to have in Web Server turned on the ``DELETE`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* There is no return value except if there is an error, the ``JSON`` [error](/v1/client-errors#error-model) object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   TeamWrapper(int tenantCode, string apiKey, string apiSecret).Delete(Guid id, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Team** id, a valid and non-empty ``guid``.
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``DELETE`` method. Default is ``false`` or use ``DELETE`` method!

Return value
------------

* If there is no error: no return value or ``void``.
* If there is an error: ``ResaultContent<Team>.Error`` object. See more in [Client Errors](/v1/client-errors).

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid teamId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper&lt;Team, TeamList&gt; teamWrapper = new TeamWrapper(tenantCode, key, secret);
   // Delete via DELETE method (default).
   ResponseContent response = teamWrapper.Delete(teamId);

   // Delete via POST method (use true argument).
   // ResponseContent response = teamWrapper.Delete(teamId, true);

   if (response.Error != null)
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
