

===========
Tenant Tree
===========

A **Tenant Tree** is a flattened representation of the whole hierachy including :ref:`tenant-label`, recursive :ref:`Units <unit-label>` and its *Managers* (:ref:`user-label`), :ref:`unit-label` :ref:`tenant-label` and its *Managers* and *Agents* which are essentially (:ref:`Users <user-label>`).

Graphical Tenant Tree Representation
====================================

..tree::

    + Tenant
    |
    |---+ Unit (recursive)
        | Unit manager(s)
        |
        |---+ Team
            | Team manager(s)
            | Agent(s)


Tenant Tree Item Model
======================

Represent the **Tenant Tree** model as flattened hierarchy with read-only properties.

.. note::

  Note that  model is used as result of read-only method *GET* (*GetTree*).


+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| Name                | Description                                                                                     | Type         |
+=====================+=================================================================================================+==============+
| ``id``              | Representing **Tenan Tree Item** identifier.                                                    | ``guid``     |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| **Common properties**                                                                                                                |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``treeItemId``      | The id of :ref:`tenant-label`, :ref:`unit-label`, :ref:`team-label` or :ref:`user-label`.       | ``guid``     |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``treeItemType``    | The item type. :ref:`tenant-label`, :ref:`unit-label`, :ref:`team-label` or :ref:`user-label`.  | ``string``   |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``name``            | The name of :ref:`tenant-label`, :ref:`unit-label`, :ref:`team-label` or :ref:`user-label`.     | ``string``   |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``isActive``        | Denotes whether the **Tenant Tree Item** state is active or inactive.                           | ``boolean``  |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``isDeleted``       | Denotes whether the **Tenant Tree Item** state is deleted or not.                               | ``boolean``  |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| **User specific**                                                                                                                    |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``recorderUserId``  | The :ref:`user-label` identification of media files within the Recorder.                        | ``string``   |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``recorderUserId``  | The :ref:`user-label` identification of media files within the Recorder.                        | ``string``   |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``haveRecorder``    | Denotes whether the [Recorder](/v1/recorder) is assigned to :ref:`user-label`.                  | ``boolean``  |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| **Manager / Agent specific**                                                                                                         |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``managerOrAgentId``| Representing the true identifier of managership/membership not only the ``userId``.             | ``guid``     |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| **Tenant specific**                                                                                                                  |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+
| ``tenantId``        | Sets to each **Tenant Tree Item** ``tenantId`` to denote which :ref:`tenant-label` it belongs.  | ``guid``     |
+---------------------+-------------------------------------------------------------------------------------------------+--------------+

.. note::

  The **Tenant Tree** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Tenant Tree** properties are capitalized (eg. ``Id``, ``Name``,..)!


Tenant Tree Item Types
^^^^^^^^^^^^^^^^^^^^^^

Currently supported [Tenant Tree](/v1/tree) item types are:

* Tenant
* Unit
* Unit Manager
* Team
* Team Manager
* Agent

Levels and Tenant Tree Item Types
---------------------------------

[Schedule](/v1/schedule) levels are essentially a **Tenant Tree** items.
But only tree items that are of type *Unit*, *Team* or *Agent* are valid as :ref:`schedule-label` ``levels``, other tree item types are invalid!


Tenant Tree Item
================

The root [Te:ref:`tenant-label` tree item with recursive items.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/tree

Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` [Tenant Tree Item Model](/v1/tree#tenant-tree-item-model).
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   TreeWrapper(int tenantCode, string apiKey, string apiSecret).GetTree();


Parameters
----------

* ``tenantCode`` :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`tenant-label` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<TenantTreeItem>.Result`` object as [Tenant Tree Item Model](/v1/tree#tenant-tree-item-model).
* If there is an error: ``ResaultContent<TenantTreeItem>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   TreeWrapper treeWrapper = new TreeWrapper(tenantCode, key, secret);
   ResponseContent<TenantTreeItem> response = treeWrapper.GetTree();

   if (response.Result != null)
   {
        // Use Result as root Tenant Tree Item.
        TenantTreeItem rootTenantItem = response.Result;

        // Root Units can be invoked
        ICollection<TenantTreeItem> rootUnits = rootTenantItem.Items;

        // .... use recursion to get full hierarchy for displaying
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
