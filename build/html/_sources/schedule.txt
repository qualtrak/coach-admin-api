.. _schedule-label:

========
Schedule
========

**Schedule** is automatically collects media for *Managers* to evaluate in the **Schedule** section of *Coach QM*.
**Schedule** essential parts are [Period Types and Occurrences](/v1/period-types) that describe the interval and type of occurrence.

Schedule Domain Model
=====================

Represent the **Schedule** domain model with available properties and its behaviors.

.. note::

  Note that domain model is used for write methods *POST* (*Create*) and *PUT* (*Update*) and as result of read-only method *GET/:id* (*GetById*).


+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| Name                              | Description                                                                                              | Type                                   | Required | Read-only | Default                 |
+===================================+==========================================================================================================+========================================+==========+===========+=========================+
| ``id``                            | Representing **Schedule** identifier.                                                                    | ``guid``                               | yes      | yes       |                         |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| **Main Details**                                                                                                                                                                                                                       |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``name``                          | The name of **Schedule**.                                                                                | ``string(500)``                        | yes      | no        |                         |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``description``                   | The description of **Schedule**.                                                                         | ``string(1024)``                       | no       | no        |                         |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``startDate``                     | The start date that triggers **Schedule**. It can be today or some date in future.                       | ``datetime``                           | yes      | no        |                         |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``maxCallPerAgent``               | The max number of media calls per *Agent*. Valid range is from 1 to 99                                   | ``short``                              | yes      | no        | ``5``                   |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``isActive``                      | Denotes whether the **Schedule** state is active or inactive.                                            | ``boolean``                            | yes      | no        | active (``false``)      |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``isArchived``                    | Denotes whether the **Schedule** state is archived or not.                                               | ``boolean``                            | yes      | no        | not archived (``false``)|
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``createdAt``                     | The **Schedule** creation date.                                                                          | ``datetime``                           | yes      | yes       |                         |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``updatedAt``                     | The date when **Schedule** was last time updated.                                                        | ``datetime``                           | yes      | yes       |                         |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``lastRunAt``                     | The date when **Schedule** was last time run by *Scheduler* engine.                                      | ``datetime``                           | no       | yes       | ``null``                |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| **Period & Occurrence**                                                                                                                                                                                                                |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``periodType``                    | The **Schedule** [Period Types](/v1/period-types).                                                       | ``byte``                               | yes      | no        | Daily (``0``)           |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``occurrenceType``                | The **Schedule** [Occurrences Types](/v1/period-types).                                                  | ``byte``                               | yes      | no        | Infinite (``0``)        |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``occurrenceTimesNumber``         | The number of times that **Schedule** will [occur](/v1/period-types).                                    | ``short``                              | no       | no        | ``0``                   |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``endDate``                       | The **Schedule** end date for [End Date Occurrence](/v1/period-types#until-end-date).                    | ``datetime``                           | no       | no        | ``null``                |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``customDateFrom``                | The **Schedule** [Custom Period date from](/v1/period-types#custom).                                     | ``datetime``                           | no       | no        | ``null``                |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``customDateTo``                  | The **Schedule** [Custom Period date to](/v1/period-types#custom).                                       | ``datetime``                           | no       | no        | ``null``                |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| **Levels & Search Criteria**                                                                                                                                                                                                           |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``levels``                        | The **Schedule** levels, see more in [Tree Item Types](/v1/tree-item-type#levels-and-item-types).        | ``array(guid)``                        | no       | no        |                         |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``searchCriteriaCollection``      | The **Schedule** collection of [Search Criteria](/v1/search-criteria).                                   | ``array(SearchCriteria)``              | no       | no        |                         |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| **Lookups**                                                                                                                                                                                                                            |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``periodTypes``                   | The dictionary of supported [Period Types](/v1/period-types#period-types).| ``dictionary(byte, string)`` | N/A                                    | N/A      | N/A      |                          |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``occurrenceTypes``               | The dictionary of supported [Occurrences](/v1/period-types#occurrences).| ``dictionary(byte, string)``   | N/A                                    | N/A      | N/A      |                          |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+
| ``searchDataTypesWithConditions`` | The collection of [Data Types and its supported Conditions](/v1/search-criteria#data-condition-model)    | ``array(SearchDataTypeWithCondition)`` | N/A      | N/A      | N/A                      |
+-----------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------+----------+-----------+-------------------------+

.. note::

  The **Schedule** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Schedule** properties are capitalized (eg. ``Id``, ``Name``,..)! \\

.. note::

  Note that *Required* properties are changed depending on wanted Period Type and Occurrence. See more in whole list of [required properties for Period Types and Occurrences](/v1/period-types#period-occurrence-required).

.. danger::

  | Beware that lookup for ``levels`` is not part of **Schedule** domain model. [Unit, Team or Agent tree item types](/v1/tree#levels-and-item-types) are valid items of [Tenant Tree](/v1/tree) to be assigned as **Schedule** ``levels``.
  | To assign values to ``levels`` you need to call [GetTree method](/v1/tree#tenant-tree-item) and use [Tenant Tree Item Model](/v1/tree#tenant-tree-item-model) ``id`` as a individual ``guid`` for ``levels``.

.. warning::

  Note that if no ``levels`` are assigned then the **Schedule** can not be active. So even the ``isActive`` is set to ``true`` and there are no ``levels`` assigned the ``isActive`` will be set to ``false``.


Schedule List Model
===================

Represent the **Schedule** list  model with available properties.

.. note::

  | The list model used only to list **Schedules** with *GET* (*GetAll*) method.
  | Note that list model can change by adding/removing properties depending what schedules of *Coach REST API* will need in future.

+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| Name                 | Description                                                                                 | Type                        |
+======================+=============================================================================================+=============================+
| ``id``               | Representing **Schedule** identifier.                                                       | ``guid``                    |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``name``             | The name of **Schedule**.                                                                   | ``string``                  |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``description``      | The **Schedule** description.                                                               | ``string``                  |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``startDate``        | The **Schedule** start date.                                                                | ``datetime``                |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``isActive``         | Denotes whether the **Schedule** state is active or inactive.                               | ``boolean``                 |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``isArchived``       | Denotes whether the **Schedule** state is archived or not.                                  | ``boolean``                 |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``periodType``       | The **Schedule** [Period Type](/v1/period-types#period-types).                              | ``string``                  |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``occurrenceType``   | The **Schedule** [Occurrence Type](/v1/period-types#occurrences).                           | ``string``                  |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``maxCallsPerAgent`` | The max number of media calls per *Agent*.                                                  | ``short``                   |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``nextRunAt``        | The **Schedule** next run at data as relative time eg. "in 2 days".                         | ``string``                  |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``lastRunAt``        | The **Schedule** last run at data as relative time eg. "2 days ago".                        | ``string``                  |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``createdSince``     | The **Schedule** creation data as relative time eg. "2 days ago".                           | ``string``                  |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``updatedSince``     | The **Schedule** data of last update as relative time eg. "2 days ago".                     | ``string``                  |
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+
| ``levels``           | The collection of [Schedule Levels List model](/v1/schedule#schedule-level-list-model).     | ``array(ScheduleLevelList)``|
+----------------------+---------------------------------------------------------------------------------------------+-----------------------------+

.. note::

  The **Schedule** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Schedule** properties are capitalized (eg. ``Id``, ``Name``,..)!


Schedule Level List Model
=========================

Represent the **Schedule** Level List model with available properties. Used as collection in  [Schedule List model](/v1/schedule#schedule-list-model).

+------------------------+---------------------------------------------------------------------------+-------------+
| Name                   | Description                                                               | Type        |
+========================+===========================================================================+=============+
| ``name``               | The *Unit*, *Team* or *Agent* name.                                       | ``string``  |
+------------------------+---------------------------------------------------------------------------+-------------+
| ``tenantTreeLevelType``| The [Unit, Team or Agent tree item type](/v1/tree#levels-and-item-types). | ``string``  |
+------------------------+---------------------------------------------------------------------------+-------------+

List of Schedules
=================

The list of **Schedules** for :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/schedules

Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` array of [Schedule List Model](/v1/schedule#schedule-list-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   ScheduleWrapper(int tenantCode, string apiKey, string apiSecret).GetAll();


Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`tenant-label` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<ICollection<Schedule>>.Result`` object as collection of the [Schedule List Model](/v1/schedule#schedule-list-model).
* If there is an error: ``ResaultContent<ICollection<Schedule>>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   IApiWrapper<Schedule, ScheduleList> scheduleWrapper = new ScheduleWrapper(tenantCode, key, secret);
   ResponseContent<ICollection<ScheduleList>> response = scheduleWrapper.GetAll();

   if (response.Result != null)
   {
        // Use Result as List of Schedules for displaying.
        ICollection<ScheduleList> schedules = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Get Schedule by Id
==================

The **Schedule** by requested Id for :ref:`tenant-label`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/schedules/:id

Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Schedule** id, a valid and non-empty ``guid``.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` as the [Schedule Domain Model](/v1/schedule#schedule-model) object.
* If there is an error: ``JSON`` as the :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   ScheduleWrapper(int tenantCode, string apiKey, string apiSecret).GetById(Guid id);


Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Schedule** id, a valid and non-empty ``guid``.

Return value
------------

* If there is no error: ``ResaultContent<Schedule>.Result`` object as the [Schedule Domain Model](/v1/schedule#schedule-model).
* If there is an error: ``ResaultContent<Schedule>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid scheduleId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper<Schedule, ScheduleList> scheduleWrapper = new ScheduleWrapper(tenantCode, key, secret);
   ResponseContent<Schedule> response = scheduleWrapper.GetById(scheduleId);

   if (response.Result != null)
   {
        // Use Result as requested Schedule for displaying.
        Schedule schedule = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Create Schedule
===============

The creation of new **Schedule** for :ref:`tenant-label`.

.. warning::

  To assign ``levels`` you'll need to get [Tenant Tree](/v1/tree) and use [Unit, Team or Agent](/v1/tree#levels-and-item-types) items as Levels!


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    POST /api/v1/:tenantCode/schedules

Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``schedule`` ``JSON`` representation of [Schedule Domain Model](/v1/schedule#schedule-model) sent via *Request HTTP Header*.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of newly created **Schedule** as the [Schedule Domain Model](/v1/schedule#schedule-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   ScheduleWrapper(int tenantCode, string apiKey, string apiSecret).Create(Schedule schedule);


Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``schedule`` The **Schedule** model constructed from **Schedule properties**.

Return value
------------

* If there is no error: ``ResaultContent<Schedule>.Result`` object as the [Schedule Domain Model](/v1/schedule#schedule-model).
* If there is an error: ``ResaultContent<Schedule>.Error`` object. See more in :ref:`client-error-label`

Example usage
-------------

.. code-block:: csharp
   :linenos:

   ICollection<Guid> levels = new List<Guid>();
   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   TreeWrapper treeWrapper = new TreeWrapper(tenantCode, key, secret);
   ResponseContent<TenantTreeItem> responseTree = treeWrapper.GetTree();

   if (responseTree.Result != null)
   {
       levels.Add(responseTree.Result.Items.Where(x => x.TreeItemType == "Unit").Select(x => x.Id).SingleOrDefault());
   }

   IApiWrapper<Schedule, ScheduleList> scheduleWrapper = new ScheduleWrapper(tenantCode, key, secret);
   // Get default data and lookup for schedules
   Schedule newSchedule = scheduleWrapper.GetById(new Guid()).Result;
   newSchedule.Name = "Tester";
   newSchedule.StartDate = DateTime.Now;
   newSchedule.Levels = levels;

   ResponseContent<Schedule> response = scheduleWrapper.Create(newSchedule);

   if (response.Result != null)
   {
        // Use Result as newly created Schedule for display.
        Schedule schedule = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Update Schedule
===============

Updates already existent **Schedule** for :ref:`tenant-label`.

.. warning::

  To assign ``levels`` you'll need to get [Tenant Tree](/v1/tree) and use [Unit, Team or Agent](/v1/tree#levels-and-item-types) items as Levels!


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    PUT /api/v1/:tenantCode/schedules/:id

Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Schedule** id, a valid and non-empty ``guid``.
* ``schedule`` ``JSON`` representation of [Schedule Domain Model](/v1/schedule#schedule-model) sent via *Request HTTP Header*.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`
  | If you don't want to have in Web Server turned on the ``PUT`` verb method read more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` representation of uodated **Schedule** as the [Schedule Domain Model](/v1/schedule#schedule-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   ScheduleWrapper(int tenantCode, string apiKey, string apiSecret).Update(Schedule schedule, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``schedule`` The **Schedule** model constructed from **Schedule properties** and ``Id`` must be provided in it. If not ``ArgumentException`` will be thrown!
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``PUT`` method. Default is ``false`` or use ``PUT`` method!

Return value
------------

* If there is no error: ``ResaultContent<Schedule>.Result`` object as the [Schedule Domain Model](/v1/schedule#schedule-model).
* If there is an error: ``ResaultContent<Schedule>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: csharp
   :linenos:

   ICollection<Guid> levels = new List<Guid>();
   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid scheduleId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   TreeWrapper treeWrapper = new TreeWrapper(tenantCode, key, secret);
   ResponseContent<TenantTreeItem> responseTree = treeWrapper.GetTree();

   if (responseTree.Result != null)
   {
       levels.Add(responseTree.Result.Items.Where(x => x.TreeItemType == "Unit").Select(x => x.Id).LastOrDefault());
   }

   IApiWrapper<Schedule, ScheduleList> scheduleWrapper = new ScheduleWrapper(tenantCode, key, secret);
   Schedule schedule = scheduleWrapper.GetById(scheduleId).Result;
   schedule.Name = "Test Schedule Updated";
   schedule.Levels = levels;

   // Update via PUT method (default).
   ResponseContent<Schedule> response = scheduleWrapper.Update(schedule);

   // Update via POST method (use true argument).
   // ResponseContent<Schedule> response = scheduleWrapper.Update(schedule, true);

   if (response.Result != null)
   {
        // Use Result of updated Schedule for display.
        Schedule updatedSchedule = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }


Delete Schedule
===============

Deletes existent **Schedule** for :ref:`tenant-label`.

.. warning::

  | Note that **Schedule** will not be deleted but rather flagged as ``isArchived`` if it was run at least once by *Schedule* engine and there are associated recordings (media) with this **Schedule**.
  | If **Schedule** has never run and there are no associated recordings (media) to it, it will be deleted permanently with all assigned **Schedule** levels.


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    DELETE /api/v1/:tenantCode/schedules/:id

Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``id`` The **Schedule** id, a valid and non-empty ``guid``.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.
  | If you don't want to have in Web Server turned on the ``DELETE`` verb method read more in :ref:`getting-started-label`


Return value
------------

* There is no return value except if there is an error, the ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   ScheduleWrapper(int tenantCode, string apiKey, string apiSecret).Delete(Guid id, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``id`` The **Schedule** id, a valid and non-empty ``guid``.
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``DELETE`` method. Default is ``false`` or use ``DELETE`` method!

Return value
------------

* If there is no error: no return value or ``void``.
* If there is an error: ``ResaultContent<Schedule>.Error`` object. See more in :ref:`client-error-label`

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";
   Guid scheduleId = new Guid("f4fe3ea7-ed2a-41dd-acd2-91c45c8b4891");

   IApiWrapper<Schedule, ScheduleList> scheduleWrapper = new ScheduleWrapper(tenantCode, key, secret);
   // Delete via DELETE method (default).
   ResponseContent response = scheduleWrapper.Delete(scheduleId);

   // DELETE via POST method (use true argument)..
   // ResponseContent response = scheduleWrapper.Delete(scheduleId, true);

   if (response.Error != null)
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
