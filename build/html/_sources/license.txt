.. _license-label:

=======
License
=======

To use *Coach QM*, there is a need to obtain valid license from *Coach Licensing Server*.

The **License** can be:

**Trial**

The trial **License** has expiry date until is valid, and after its expired, the access to *Coach QM* is denied for all users, but *Coach Console* is still accessible and fully functional.

**Forever**

The **License** last forever and it has count of bought **Licenses** that is subtracted for every creation of an active agent. When the count is exceeded, there is no way to make active agents, except of buying more licenses.

.. note::

  Note that the information of Expiry Date of **License**, Available and Used **Licenses** you can get through :ref:`tenant-label` properties.


Obtain License
==============

Obtains **License** for :ref:`Current Tenant <tenant-label>`.

.. danger::

  Beware that :ref:`tenant-label` properties ``customerId`` and ``customerCode`` needs to be updated with values given by *Qualtrak* received upon **License** purchase or on request for trial **License**.


Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/license

Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.

.. danger::

  Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in [Getting Started](/v1).


Return value
------------

* There is no return value except if there is an error, the ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: c#
   :linenos:

   LicenseWrapper(int tenantCode, string apiKey, string apiSecret).Obtain();


Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`Current Tenant <tenant-label>` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`Current Tenant <tenant-label>` API Secret provided by **Qualtrak**.

Return value
------------

* If there is no error: no return value or ``void``.
* If there is an error: ``ResaultContent<ICollection<MediaPlayer>>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: c#
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   LicenseWrapper licenseWrapper = new LicenseWrapper(tenantCode, key, secret);
   ResponseContent response = licenseWrapper.Obtain();

   if (response.Error != null)
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
