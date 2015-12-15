.. _user-label:

====
User
====

A **User** is an individual within the organization. They can be assigned any *Role* but most will be designated as an *Agent* or as the *Manager* of a :ref:`team-label` and/or :ref:`unit-label`.
A **User** can be n *Manager*, *Agent* or *unassigned*. The *unassigned* users are not visible in hierarchical tree, see more in [Tenant Tree](/v1/tree).

.. note::

  The number of **Users** that can be added to a :ref:`tenant-label` is not limited but the number that can be activated is restricted to the number of licenses that have been purchased. For more information see [Licensing](/v1/licensing).


User Domain Model
=================

Represent the **User** domain model with available properties and its behaviors.

.. note::

  Note that domain model is used for write methods *POST* (*Create*) and *PUT* (*Update*) and as result of read-only method *GET/:id* (*GetById*).


+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| Name                             | Description                                                                            | Type                          | Required | Read-only    | Default                 |
+==================================+========================================================================================+===============================+==========+==============+=========================+
| ``id``                           | Representing **User** identifier.                                                      | ``guid``                      | yes      | yes          |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| **Personal Details**                                                                                                                                                                                          |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``username``                     | The username of **User**.                                                              | ``string(102)``               | yes      | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``firstName``                    | The **User** first name.                                                               | ``string(50)``                | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``lastName``                     | The **User** last name.                                                                | ``string(50)``                | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``email``                        | The **User** email.                                                                    | ``string(100)``               | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``phone``                        | The **User** phone number.                                                             | ``string(30)``                | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``address``                      | The **User** residing address.                                                         | ``string(255)``               | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``country``                      | The **User** residing country.                                                         | ``string(50)``                | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``dateOfBirth``                  | The **User** date of birth.                                                            | ``datetime``                  | no       | no           | ``null``                |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``isActive``                     | Denotes whether the **User** state is active or inactive.                              | ``boolean``                   | yes      | no           | active (``true``)       |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``isDeleted``                    | Denotes whether the **User** state is deleted or not.                                  | ``boolean``                   | yes      | [partially]  | not deleted (``false``) |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| **Employee Details**                                                                                                                                                                                          |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``employeeReference``            | E.g. Payroll number or another unique identifier.                                      | ``string(50)``               | no       | no            |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``startDate``                    | The **User** employment start date.                                                    | ``datetime``                 | no       | no            | ``null``                |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``endDate``                      | The **User** employment end date.                                                      | ``datetime``                 | no       | no            | ``null``                |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| **Recorder**                                                                                                                                                                                                  |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``recorderPlayerId``             | The [Recorder](/v1/unit) where the **User’s** media files are                          | ``guid``                      | no       | no           | ``null``                |
|                                  | recorded and stored.                                                                   |                               |          |              |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``recorderUserId``               | The **User** identification of media files within the [Recorder](/v1/recorder).        | ``string(500)``               | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``recorderAccountId``            |                                                                                        | ``string(500)``               | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| **User Managerships,**           | **Memberships and Roleships**                                                                                                                                              |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``managedUnits``                 | The **User's** managed [Units](/v1/unit).                                              | ``array(guid)``               | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``managedTeams``                 | The **User's** managed [Teams](/v1/team).                                              | ``array(guid)``               | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``teamMemberships``              | The **User's** :ref:`team-label` memberships.                                          | ``array(guid)``               | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``roles``                        | The **User's** assigned :ref:`roles-label`                                             | ``array(guid)``               | no       | no           |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| **Lookups**                                                                                                                                                                                                   |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``unitsLookup``                  | The dictionary of active and not deleted [Units](/v1/unit),                            | ``dictionary(guid, string)``  | N/A      | N/A          | N/A                     |
|                                  | needed for setting the ``managedUnits``.                                               |                               |          |              |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``teamsLookup``                  | The dictionary of active and not deleted [Teams](/v1/team), needed for                 | ``dictionary(guid, string)``  | N/A      | N/A          | N/A                     |
|                                  | setting the **User's** ``managedTeams`` and ``teamMembership``.                        |                               |          |              |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``rolesLookup``                  | The dictionary of only adminstrative roles, needed                                     | ``dictionary(guid, string)``  | N/A      | N/A          | N/A                     |
|                                  | for setting the **User's** ``roles``. Read more in :ref:`roles-label` .                |                               |          |              |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+
| ``recorderMediaPlayersLookup``   | The dictionary of active [Recorders](/v1/recorder),                                    | ``dictionary(guid, string)``  | N/A      | N/A          | N/A                     |
|                                  | needed for setting the **User's** ``recorerPlayerId``.                                 |                               |          |              |                         |
+----------------------------------+----------------------------------------------------------------------------------------+-------------------------------+----------+--------------+-------------------------+

.. note::

  The **User** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **User** properties are capitalized (eg. ``Id``, ``Name``,..)!



.. warning::

 | **Active and Deleted Logic**
 |
 | When **User** is deleted by [Delete](/v1/user#user-delete) command and it is flagged as ``isDeleted`` as ``true`` and also by default it is flagged ``isActive`` as ``false``. Note that  status ``isActive`` will remain "*locked*" until the **User's** ``isDeleted`` state is updated to ``false`` or *not deleted* anymore. Then ``isActive`` is "*unlocked*" and can be changed. If the **User** is *deleted* and on update is tried to change ``isActive`` property, server will silently ignore sent ``isActive`` property.
 |
 | Managed [Unit(s)](/v1/unit), Managed [Team(s)](/v1/team) and [Administrative Role(s)](/v1/roles) can be set to only *active* and *not deleted* **Users**. If is sent otherwise to *inactive* and/or *deleted* **User**, server will silently ignore those assignments.


User List Model
===============

Represent the **User** list  model with available properties.

.. note::

  | The list model used only to list **Users** with *GET* (*GetAll*) method.
  | Note that list model can change by adding/removing properties depending what users of *Coach REST API* will need in future.


+----------------------+----------------------------------------------------------------------+-----------------+
| Name                 | Description                                                          | Type            |
+======================+======================================================================+=================+
| ``id``               | Representing **User** identifier.                                    | ``guid``        |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``username``         | The username of **User**.                                            | ``string``      |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``firstName``        | The **User** first name.                                             | ``string``      |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``lastName``         | The **User** last name.                                              | ``string``      |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``isActive``         | Denotes whether the **User** state is active or inactive.            | ``boolean``     |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``isDeleted``        | Denotes whether the **User** state is deleted or not.                | ``boolean``     |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``recorderUserId``   | The **User** identification of media files within the Recorder.      | ``string``      |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``recorderAccountId``|                                                                      | ``string(50)``  |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``managedUnits``     | The **User's** managed :ref:`Units <unit-label>` comma separated.    | ``string``      |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``managedTeams``     | The **User's** managed :ref:`Teams <team-label>` comma separated.    | ``string``      |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``teamMemberships``  | The **User's** :ref:`team-label` memberships comma separated.        | ``string``      |
+----------------------+----------------------------------------------------------------------+-----------------+
| ``assignedRoles``    | The **User's** assigned :ref:`roles-label` comma separated.          | ``string``      |
+----------------------+----------------------------------------------------------------------+-----------------+

.. note::

  The **User** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **User** properties are capitalized (eg. ``Id``, ``Name``,..)!


List of Users
=============

The list of **Users** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/users

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------
* If there is no error: ``JSON`` array of [User List Model](/v1/user#user-list-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UserWrapper(int tenantCode, string apiKey, string apiSecret).GetAll();

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<ICollection<User>>.Result`` object as collection of the [User List Model](/v1/user#user-list-model).
* If there is an error: ``ResaultContent<ICollection<User>>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   ITreeApiWrapper<User, UserList> userWrapper = new UserWrapper(tenantCode, key, secret);
   ResponseContent<ICollection<UserList>> response = userWrapper.GetAll();

   if (response.Result != null)
   {
        // Use Result as List of Users for displaying.
        ICollection<UserList> users = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }

Get User by Id
==============

The **User** by requested Id for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/users/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **User** id, a valid and non-empty ``guid``.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.

Return value
------------

* If there is no error: ``JSON`` as the [User Domain Model](/v1/user#user-model) object.
* If there is an error: ``JSON`` as the :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UserWrapper(int tenantCode, string apiKey, string apiSecret).GetById(Guid id);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **User** id, a valid and non-empty ``guid``.

Return value
------------

* If there is no error: ``ResaultContent<User>.Result`` object as the [User Domain Model](/v1/user#user-model).
* If there is an error: ``ResaultContent<User>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid userId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   ITreeApiWrapper<User, UserList> userWrapper = new UserWrapper(tenantCode, key, secret);
   ResponseContent<User> response = userWrapper.GetById(userId);

   if (response.Result != null)
   {
        // Use Result as requested User for displaying.
        User user = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Create User
===========

The creation of new **User** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    POST /api/v1/:tenantCode/users

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``user`` ``JSON`` representation of [User Domain Model](/v1/user#user-model) sent via *Request HTTP Header*.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of newly created **User** as the [User Domain Model](/v1/user#user-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UserWrapper(int tenantCode, string apiKey, string apiSecret).Create(User user);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``user`` The **User** model constructed from **User properties**.

Return value
------------

* If there is no error: ``ResaultContent<User>.Result`` object as the [User Domain Model](/v1/user#user-model).
* If there is an error: ``ResaultContent<User>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   ITreeApiWrapper<User, UserList> userWrapper = new UserWrapper(tenantCode, key, secret);
   // Get default data and lookup for users
   User newUser = userWrapper.GetById(new Guid()).Result;
   newUser.Username = "Tester";
   newUser.RecorderMediaPlayerId = newUser.RecorderMediaPlayersLookup.FirstOrDefault().Key;
   newUser.Roles = new List<Guid> { newUser.RolesLookup.FirstOrDefault().Key };
   newUser.ManagedUnits = new List<Guid> { newUser.UnitsLookup.FirstOrDefault().Key };
   newUser.ManagedTeams = new List<Guid> { newUser.TeamsLookup.FirstOrDefault().Key };
   newUser.TeamMemberships = new List<Guid> { newUser.TeamsLookup.LastOrDefault().Key };

   ResponseContent<User> response = userWrapper.Create(newUser);

   if (response.Result != null)
   {
        // Use Result as newly created User for display.
        User user = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Update User
===========

Updates already existent **User** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    PUT /api/v1/:tenantCode/users/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **User** id, a valid and non-empty ``guid``.
* ``user`` ``JSON`` representation of [User Domain Model](/v1/user#user-model) sent via *Request HTTP Header*.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.
  | If you don't want to have in Web Server turned on the ``PUT`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of uodated **User** as the [User Domain Model](/v1/user#user-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UserWrapper(int tenantCode, string apiKey, string apiSecret).Update(User user, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``user`` The **User** model constructed from **User properties** and ``Id`` must be provided in it. If not ``ArgumentException`` will be thrown!
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``PUT`` method. Default is ``false`` or use ``PUT`` method!

Return value
------------

* If there is no error: ``ResaultContent<User>.Result`` object as the [User Domain Model](/v1/user#user-model).
* If there is an error: ``ResaultContent<User>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid userId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   ITreeApiWrapper<User, UserList> userWrapper = new UserWrapper(tenantCode, key, secret);
   User user = userWrapper.GetById(userId).Result;
   user.Username = "Tester";
   user.RecorderMediaPlayerId = user.RecorderMediaPlayersLookup.FirstOrDefault().Key;
   user.Roles = new List<Guid> { user.RolesLookup.FirstOrDefault().Key };
   user.ManagedUnits = new List<Guid> { user.UnitsLookup.FirstOrDefault().Key };
   user.ManagedTeams = new List<Guid> { user.TeamsLookup.FirstOrDefault().Key };
   user.TeamMemberships = new List<Guid> { user.TeamsLookup.LastOrDefault().Key };

   // Update via PUT method (default).
   ResponseContent<User> response = userWrapper.Update(user);

   // Update via POST method (use true argument).
   // ResponseContent<User> response = userWrapper.Update(user, true);

   if (response.Result != null)
   {
        // Use Result of updated User for display.
        User updatedUser = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Delete User
===========

Deletes existent **User** for current :ref:`tenant-label`.

.. warning::

  | Note that if **User** is a *Unit Manager*, *Team Manager*, *Agent* or has some [Role](/v1/roles) assigned to it then **User** will not be deleted but flagged as ``isDeleted``. When **User** is deleted it can be undeleted by setting ``isDeleted`` to ``false`` while updating **Unit**.
  | If **User** is not a *Unit Manager*, *Team Manager*, *Agent* or has no [Role](/v1/roles) assigned to it, it will be deleted permanently.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    DELETE /api/v1/:tenantCode/users/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **User** id, a valid and non-empty ``guid``.

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

   UserWrapper(int tenantCode, string apiKey, string apiSecret).Delete(Guid id, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **User** id, a valid and non-empty ``guid``.
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``DELETE`` method. Default is ``false`` or use ``DELETE`` method!

Return value
------------

* If there is no error: no return value or ``void``.
* If there is an error: ``ResaultContent<User>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid userId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   ITreeApiWrapper<User, UserList> userWrapper = new UserWrapper(tenantCode, key, secret);
   // Delete via DELETE method (default).
   ResponseContent response = userWrapper.Delete(userId);

   // DELETE via POST method (use true argument)..
   // ResponseContent response = userWrapper.Delete(userId, true);

   if (response.Error != null)
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
