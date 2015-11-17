.. _client-error-label:

====================
Client Errors
====================

The description of client side errors that can get from *REST API* server on known logic errors and unknown exceptions.

Error Model
===========

Represents the **Error** model as value object with available properties.

+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+
| Name                | Description                                                                                               | Type                       |
+=====================+===========================================================================================================+============================+
| ``id``              | Representing **Error** identifier from API Logs.                                                          | ``guid``                   |
+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+
| ``message``         | The **Error** message it can be descriptive for known error and generic for unknown exceptions.           | ``string``                 |
+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+
| ``description``     | The **Error** description mainly a generic text for unknown exception.                                    | ``string``                 |
+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+
| ``httpStatusCode``  | The HTTP Status Code, eg. 200.                                                                            | ``integer``                |
+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+
| ``requestArguments``| The collection of sent Request Arguments.                                                                 | ``array(RequestArgument)`` |
+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+

.. hint::

    The **Error** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Error** properties are capitalized (eg. ``Id``, ``Name``,..)!

    Note that C# Wrapper has for **Error** Model overridden a ``ToString()`` method and calling instance of error like ``error.ToString()`` will result with displaying the **Error** and all **Requested Arguments**

.. warning::

    Note that only simple **Request Arguments** will be sent like ``integer``, ``string``, ``boolean``,... The complex types are currently not supported to be sent as **Error** **Request Arguments**.

Request Argument Model
======================

Represents the **Request Argument** model as value object with available properties.

+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+
| Name                | Description                                                                                               | Type                       |
+=====================+===========================================================================================================+============================+
| ``name``            | The **Request Argument** name, eg. ``id``.                                                                | ``string``                 |
+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+
| ``value``           | The **Request Argument** value for ``name`` **Request Argument**.                                         | ``string``                 |
+---------------------+-----------------------------------------------------------------------------------------------------------+----------------------------+


.. hint::

    The **Error** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Error** properties are capitalized (eg. ``Id``, ``Name``,..)!

Known Errors
============

The list of **Known Errors** that can happen while interacting with *Coach REST API*.

.. hint::

    Note that this errors are generic description of server side known errors and errors sent to client will be with proper and very descriptive error messages, due to some logic and according to what arguments are sent when error occurred.
    Many errors are more described in particular entity's documentation, mostly around its Domain Model.

+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| Known Error                              | Description                                                                                                       |
+==========================================+===================================================================================================================+
| **Missing Consumer Key and/or Secret**   | Consumer key and/or secret is not sent with HTTP Header.                                                          |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Unauthorized Key and/or Secret**       | Consumer key/secret combination is not known and hence unauthorized.                                              |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Invalid Tenant Code**                  | The tenant code provided through URL is not valid. Must be 1000 and greater!                                      |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Unknown Tenant Code**                  | The tenant code is not existing.                                                                                  |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Unknown Content-Type**                 | The Request Header must include a valid and supported Content-Type media format (JSON or XML).                    |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Exceeded License Total For Agents**    | The licenses exceeded the total of purchased licenses. Note one active user as agent is one license!              |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Unknown Reference Entity Id**          | The sent referenced entity GUID Id is unknown or empty GUID. Reference to entity can be established.              |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Unique Username**                      | Validates the uniqueness of User's username. There cannot be two same usernames for tenant.                       |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Required Field**                       | Validates that required field or property has proper value assigned to it.                                        |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Invalid Id**                           | The Id of entity is empty GUID.                                                                                   |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Invalid Date Range**                   | The date range of start and end date is invalid when end date is greater than start date.                         |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Incorrect Period Type**                | The incorrect combination usage of schedule period type and occurrence.                                           |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Incorrect Numeric**                    | The applied numeric value is not correct whether of crossing some range, negative number, greater than 0,...      |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Incorrect Date**                       | The applied data is no correct due some date logic.                                                               |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| **Delete While Having Reference**        | The entities that are referenced by some other entities are not allowed to be deleted.                            |
+------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
