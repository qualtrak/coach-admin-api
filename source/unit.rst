.. _unit-label:

====
Unit
====

The **Unit** is part of :ref:`tenant-label`. A **Unit** may be a department or contact center within an organization. Each **Unit** may contain one or more other organizational sub-units and act as a **"Parent Unit"** to them.

Unit Domain Model
=================

Represent the **Unit** domain model with available properties and its behaviors.

.. note::

  Note that domain model is used for write methods *POST* (*Create*) and *PUT* (*Update*) and as result of read-only method *GET/:id* (*GetById*).


+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| Name               | Description                                                       | Type                                | Required | Read-only        | Default                   |
+====================+===================================================================+=====================================+==========+==================+===========================+
| ``id``             | Representing **Unit** identifier.                                 | ``guid``                            | yes      | yes              |                           |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| ``name``           | The name of **Unit**.                                             | ``string(50)``                      | yes      | no               |                           |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| ``description``    | The description of **Unit**.                                      | ``string(255)``                     | no       | no               |                           |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| ``isActive``       | Denotes whether the **Unit** state is active or inactive.         | ``boolean``                         | yes      | no               | active (``true``)         |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| ``isDeleted``      | Denotes whether the **Unit** state is deleted or not.             | ``boolean``                         | yes      | [partially]      | not deleted (``false``)   |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| ``parentUnitId``   | Represent the hierarchical parent of **Unit**. If there           | ``guid``                            | no       | no               | Unit is root (``null``)   |
|                    | is no parent **Unit**, then **Unit** is root.                     |                                     |          |                  |                           |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| ``managers``       | The **Unit** assigned [Managers (User)](/v1/user).                | ``array(guid)``                     | no       | no               |                           |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| **Lookups**                                                                                                                                                                            |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| ``unitsLookup``    | The dictionary of active and not deleted **Units**,               | ``dictionary(guid, string)``        | N/A      | N/A              | N/A                       |
|                    | needed for choosing parent **Unit** and setting ``parentUnitId``. |                                     |          |                  |                           |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+
| ``usersLookup``    | The dictionary of active and not deleted :ref:`Users <user-label>`| ``dictionary(guid, string)``        | N/A      | N/A              | N/A                       |
|                    | needed for setting the **Unit** ``managers``.                     |                                     |          |                  |                           |
+--------------------+-------------------------------------------------------------------+-------------------------------------+----------+------------------+---------------------------+

.. note::

  The **Unit** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Unit** properties are capitalized (eg. ``Id``, ``Name``,..)!


.. warning::

  | **Active and Deleted Logic**
  |
  | When **Unit** is deleted by [Delete command](/v1/unit#unit-delete) and it is flagged as ``isDeleted`` as ``true`` and also by default it is flagged ``isActive`` as ``false``. Note that  status ``isActive`` will remain "*locked*" until the **Unit's** ``isDeleted`` state is updated to ``false`` or *not deleted* anymore. Then ``isActive`` is "*unlocked*" and can be changed. If the **Unit** is *deleted* and on update is tried to change ``isActive`` property, server will silently ignore sent ``isActive`` property.
  |
  | [Unit Manager(s)](/v1/user) and parent **Unit** can be set to only *active* and *not deleted* **Units**. If is sent otherwise to *inactive* and/or *deleted* **Unit**, server will silently ignore those assignments.


Unit List Model
===============

Represent the **Unit** list model with available properties.

.. note::

  | The list model used only to list **Units** with *GET* (*GetAll*) method.
  | Note that list model can change by adding/removing properties depending what users of *Coach REST API* will need in future.


+--------------------+--------------------------------------------------------------------------------------------+-------------+
| Name               | Description                                                                                | Type        |
+====================+============================================================================================+=============+
| ``id``             | Representing **Unit** identifier.                                                          | ``guid``    |
+--------------------+--------------------------------------------------------------------------------------------+-------------+
| ``name``           | The name of **Unit**.                                                                      | ``string``  |
+--------------------+--------------------------------------------------------------------------------------------+-------------+
| ``description``    | The description of **Unit**.                                                               | ``string``  |
+--------------------+--------------------------------------------------------------------------------------------+-------------+
| ``isActive``       | Denotes whether the **Unit** state is active or inactive.                                  | ``boolean`` |
+--------------------+--------------------------------------------------------------------------------------------+-------------+
| ``isDeleted``      | Denotes whether the **Unit** state is deleted or not.                                      | ``boolean`` |
+--------------------+--------------------------------------------------------------------------------------------+-------------+
| ``parentUnitName`` | The name of **Unit** parent. Needed for representing the parent unit in list of Units.     | ``string``  |
+--------------------+--------------------------------------------------------------------------------------------+-------------+

.. note::

  The **Unit** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Unit** properties are capitalized (eg. ``Id``, ``Name``,..)!


List of Units
=============

The list of **Units** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/units

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer key* and *API Secret* as *customer secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` array of [Unit List Model](/v1/unit#unit-list-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UnitWrapper(int tenantCode, string apiKey, string apiSecret).GetAll();

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<ICollection<UnitList>>.Result`` object as collection of the [Unit List Model](/v1/unit#unit-list-model).
* If there is an error: ``ResaultContent<ICollection<UnitList>>.Error`` object. See more in :ref:`client-error-label` .

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   IApiWrapper<Unit, UnitList>unitWrapper = new UnitWrapper(tenantCode, key, secret);
   ResponseContent<ICollection<UnitList>> response = unitWrapper.GetAll();

   if (response.Result != null)
   {
        // Use Result as List of Units for displaying.
        ICollection&lt;UnitList&gt; units = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Get Unit by Id
==============

The **Unit** by requested Id for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/units/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Unit** id, a valid and non-empty ``guid``.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` as the [Unit Domain Model](/v1/unit#unit-model) object.
* If there is an error: ``JSON`` as the :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UnitWrapper(int tenantCode, string apiKey, string apiSecret).GetById(Guid id);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Unit** id, a valid and non-empty ``guid``.

Return value
------------

* If there is no error: ``ResaultContent<Unit>.Result`` object as the [Unit Domain Model](/v1/unit#unit-model).
* If there is an error: ``ResaultContent<Unit>.Error`` object. See more in :ref:`client-error-label` .

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid unitId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper<Unit, UnitList> unitWrapper = new UnitWrapper(tenantCode, key, secret);
   ResponseContent<Unit> response = unitWrapper.GetById(unitId);

   if (response.Result != null)
   {
        // Use Result as requested Unit for displaying.
        Unit unit = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }

Create Unit
===========

The creation of new **Unit** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    POST /api/v1/:tenantCode/units

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``unit`` ``JSON`` representation of [Unit Domain Model](/v1/unit#unit-model) sent via *Request HTTP Header*.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of newly created **Unit** as the [Unit Domain Model](/v1/unit#unit-model).
* If there is an error: ``JSON`` :ref:`client-error-label`  object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UnitWrapper(int tenantCode, string apiKey, string apiSecret).Create(Unit unit);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``unit`` The **Unit** model constructed from [Unit Domain Model](/v1/unit#unit-model).

Return value
------------

* If there is no error: ``ResaultContent<Unit>.Result`` object as the [Unit Domain Model](/v1/unit#unit-model).
* If there is an error: ``ResaultContent<Unit>.Error`` object. See more in :ref:`client-error-label` .

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   IApiWrapper<Unit, UnitList> unitWrapper = new UnitWrapper(tenantCode, key, secret);
   // Get default data and lookup for units
   Unit newUnit = unitWrapper.GetById(new Guid()).Result;
   newUnit.Name = "Unit created from test";
   newUnit.Description = "Unit created from test description.";
   // Set parent Unit key from units lookup key.
   newUnit.ParentUnitId = newUnit.UnitsLookup.FirstOrDefault().Key;
   ResponseContent<Unit> response = unitWrapper.Create(newUnit);

   if (response.Result != null)
   {
        // Use Result as newly created Unit for display.
        Unit unit = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Update Unit
===========

Updates already existent **Unit** for current :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    PUT /api/v1/:tenantCode/units/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Unit** id, a valid and non-empty ``guid``.
* ``unit`` ``JSON`` representation of [Unit Domain Model](/v1/unit#unit-model) sent via *Request HTTP Header*.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.
  | If you don't want to have in Web Server turned on the ``PUT`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of uodated **Unit** as the [Unit Domain Model](/v1/unit#unit-model).
* If there is an error: ``JSON`` :ref:`client-error-label`  object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UnitWrapper(int tenantCode, string apiKey, string apiSecret).Update(Unit unit, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``unit`` The **Unit** model constructed from [Unit Domain Model](/v1/unit#unit-model) and ``Id`` must be provided in it. If not ``ArgumentException`` will be thrown!
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``PUT`` method. Default is ``false`` or use ``PUT`` method!

Return value
------------

* If there is no error: ``ResaultContent<Unit>.Result`` object as the [Unit Domain Model](/v1/unit#unit-model).
* If there is an error: ``ResaultContent<Unit>.Error`` object. See more in :ref:`client-error-label` .

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid unitId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper<Unit, UnitList> unitWrapper = new UnitWrapper(tenantCode, key, secret);
   Unit unit = unitWrapper.GetById(unitId).Result;
   unit.Name = "Unit updated from test";
   unit.Description = "Unit updated from test description.";
   // Set parent Unit key from units lookup key.
   unit.ParentUnitId = unit.UnitsLookup.FirstOrDefault().Key;

   // Update via PUT method (default).
   ResponseContent<Unit> response = unitWrapper.Update(unit);

   // Update via POST method (use true argument).
   // ResponseContent&lt;Unit&gt; response = unitWrapper.Update(unit, true);

   if (response.Result != null)
   {
        // Use Result of updated Unit for display.
        Unit updatedUnit = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Delete Unit
===========

Deletes existent **Unit** for current :ref:`tenant-label`.

.. warning::

  | Note that if **Unit** is parent to the other **Units** or there are any :ref:`Teams <team-label>` belonging to it or assigned *Unit Managers* then **Unit** will not be deleted but flagged as ``isDeleted``. When **Unit** is deleted it can be undeleted by setting ``isDeleted`` to ``false`` while updating **Unit**. \\
  | If **Unit** has no child **Units**, :ref:`Teams <team-label>` or *Unit Managers*, it will be deleted permanently.


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    DELETE /api/v1/:tenantCode/units/:id

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Unit** id, a valid and non-empty ``guid``.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.
  | If you don't want to have in Web Server turned on the ``DELETE`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* There is no return value except if there is an error, the ``JSON`` :ref:`client-error-label`  object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   UnitWrapper(int tenantCode, string apiKey, string apiSecret).Delete(Guid id, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Unit** id, a valid and non-empty ``guid``.
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``DELETE`` method. Default is ``false`` or use ``DELETE`` method!

Return value
------------

* If there is no error: no return value or ``void``.
* If there is an error: ``ResaultContent<Unit>.Error`` object. See more in :ref:`client-error-label` .

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid unitId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper<Unit, UnitList> unitWrapper = new UnitWrapper(tenantCode, key, secret);
   // Delete via DELETE method (default).
   ResponseContent response = unitWrapper.Delete(unitId);

   // Delete via POST method (use true argument).
   // ResponseContent response = unitWrapper.Delete(unitId, true);

   if (response.Error != null)
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
