.. _tenant-label:

======
Tenant
======

The **Tenant** is the organization. A **Tenant** must be created before any other step can be taken and this step will be performed during the initial installation process. The structure of the company can be replicated within the make-up of the **Tenant** through :ref:`unit-label` and :ref:`Teams <team-label>`.

Whenever a **Tenant** is created, part of the process involves the creation of a unique administrative :ref:`user-label`. For the original host **Tenant**, setup during the **Coach** installation process, this :ref:`user-label` is a *System Administrator*. With all additional **Tenants** this built in :ref:`user-label` will be an *Application Administrator*. See more information in [Roles](/v1/roles).

.. danger::

  Only a System Administrator has the permission to create, edit and delete **Tenants**, though an *Application Administrator* can edit all of their own **Tenant’s** properties.

.. danger::

 | Note that multi-tenancy or create and delete of **Tenant** is currently not supported through *API*, but it will be soon!
 | With multi-tenancy implementation except *API* breaking changes for *REST* and *C# Wrapper* approach!!!


Tenant Domain Model
===================

Represent the **Tenant** domain model with available properties and its behaviors.

.. note::

  Note that domain model is used for write methods *POST* (*Create*) and *PUT* (*Update*) and as result of read-only method *GET/:id* (*GetById*).


+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| Name                      | Description                                                    | Type                         | Required | Read-only | Default                 |
+===========================+================================================================+==============================+==========+===========+=========================+
| ``id``                    | Representing **Tenant** identifier.                            | ``guid``                     | yes      | yes       |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| **Tenant Details**                                                                                                                                                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``name``                  | The name of **Tenant**.                                        | ``string(50)``               | yes      | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``description``           | The **Tenant** description.                                    | ``string(50)``               | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``email``                 | The **Tenant** email.                                          | ``string(50)``               | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``phone``                 | The **Tenant** phone number.                                   | ``string(50)``               | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``address``               | The **Tenant** residing address.                               | ``string(50)``               | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``mainContact``           | The **Tenant** main contact person.                            | ``string(50)``               | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``isActive``              | Denotes whether the **Tenant** state is active or inactive.    | ``boolean``                  | yes      | no        | active (``true``)       |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``isDeleted``             | Denotes whether the **Tenant** state is deleted or not.        | ``boolean``                  | yes      | yes       | not deleted (``false``) |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| **Branding**                                                                                                                                                               |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``customNameForTenant``   | Branded replacement name for word "Tenant", affects *QM* UI.   | ``string(30)``               | no       | no        | ``Tenant``              |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``customNameForUnit``     | Branded replacement name for word "Unit", affects *QM* UI.     | ``string(30)``               | no       | no        | ``Unit``                |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``customNameForTemplate`` | Branded replacement name for "Template", affects *QM* UI.      | ``string(30)``               | no       | no        | ``Template``            |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| **Licensing**                                                                                                                                                              |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``customerId``            |                                                                | ``string(50)``               | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``customerCode``          |                                                                | ``string(50)``               | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``licenseExpiryDate``     | The **Tenant** license expiry date.                            | ``datetime``                 | N/A      | yes       | `null`                  |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``totalLicenses``         | The number of :ref:`user-label` total licenses for **Tenant**. | ``integer``                  | N/A      | yes       |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``usedLicenses``          | The number of used licenses for **Tenant**.                    | `integer`                    | N/A      | yes       |                         |
|                           | One :ref:`user-label` equals  one license.                     |                              |          |           |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| **API**                                                                                                                                                                    |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``apiKey``                | The API key for **Tenant**.                                    | ``string``                   | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+
| ``apiSecret``             | The API secret for **Tenant**.                                 | ``string``                   | no       | no        |                         |
+---------------------------+----------------------------------------------------------------+------------------------------+----------+-----------+-------------------------+


.. note::

  The **Tenant** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **User** properties are capitalized (eg. ``Id``, ``Name``,..)!


Get Tenant by Id
================

The **Tenant** by requested Id.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/tenants/:tenantCode

Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in [Authentication](/v1/authentication).


Return value
------------

* If there is no error: ``JSON`` as the [Tenant Domain Model](/v1/tenant#tenant-model) object.
* If there is an error: ``JSON`` as the [error](/v1/client-errors#error-model) object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   TenantWrapper(int tenantCode, string apiKey, string apiSecret).GetByCode(int tenantCode);

Parameters
----------

* ``tenantCode`` The **Tenant** code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: ``ResaultContent<Tenant>.Result`` object as the [Tenant Domain Model](/v1/tenant#tenant-model).
* If there is an error: ``ResaultContent<Tenant>.Error`` object. See more in [Client Errors](/v1/client-errors).

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   TenantWrapper tenantWrapper = new TenantWrapper(tenantCode, key, secret);
   ResponseContent<Tenant> response = tenantWrapper.GetByCode(tenantCode);

   if (response.Result != null)
   {
        // Use Result as requested Tenant for displaying.
        Tenant tenant = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }

Update Tenant
=============

Updates already existent **Tenant**.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    PUT /api/v1/:tenantCode/tenants/:tenantCode

Parameters
----------

* ``tenantCode`` The **Tenant** code, a valid ``integer`` greater or equal to 1000.
* ``tenant`` ``JSON`` representation of [Tenant Domain Model](/v1/tenant#tenant-model) sent via *Request HTTP Header*.

.. danger::

  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in [Authentication](/v1/authentication).
  | If you don't want to have in Web Server turned on the `PUT` verb method read more in :ref:`getting-started-label`.

Return value
------------

* If there is no error: ``JSON`` representation of uodated **Tenant** as the [Tenant Domain Model](/v1/tenant#tenant-model).
* If there is an error: ``JSON`` [error](/v1/client-errors#error-model) object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#

   TenantWrapper(int tenantCode, string apiKey, string apiSecret).Update(Tenant tenant, bool updateViaPost = false);


Parameters
----------

* ``tenantCode`` Current :ref:`tenant-label` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` Current :ref:`tenant-label` API Key provided by **Qualtrak**.
* ``apiSecret`` Current :ref:`tenant-label` API Secret provided by **Qualtrak**.
* ``tenant`` The **Tenant** model constructed from **Tenant properties** and ``Id`` must be provided in it. If not ``ArgumentException`` will be thrown!
* ``updateViaPost`` Set to ``true`` if in your Web Server you don't want to enable ``PUT`` method. Default is ``false`` or use ``PUT`` method!

Return value
------------

* If there is no error: ``ResaultContent<Tenant>.Result`` object as the [Tenant Domain Model](/v1/tenant#tenant-model).
* If there is an error: ``ResaultContent<Tenant>.Error`` object. See more in [Client Errors](/v1/client-errors).

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   TenantWrapper tenantWrapper = new TenantWrapper(tenantCode, key, secret);
   Tenant tenant = tenantWrapper.GetByCode(tenantCode).Result;
   tenant.name = "Tenant Updated";

   // Update via PUT method (default).
   ResponseContent<Tenant> response = tenantWrapper.Update(tenant);

   // Update via POST method (use true argument).
   // ResponseContent&lt;Tenant&gt; response = tenantWrapper.Update(tenant, true);

   if (response.Result != null)
   {
        // Use Result of updated Tenant for display.
        Tenant updatedTenant = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
