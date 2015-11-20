.. _search-criteria-label:

===============
Search Criteria
===============

The **search criteria** are the parameters that a *Manager* can use to search for individual recordings for evaluation in *Coach QM* and it is used for [Schedule](/v1/schedule). These parameters can be configured to reflect any type of search that can be performed within the :ref:`recorder-label` itself, allowing for a seamless user experience between the integrated applications. As few or as many search criteria can be configured as required.

Search Criteria Model
=====================

Represents the **Search Criteria** model as value object with available properties and its behaviors used for :ref:`recorder-label` and [Schedule](/v1/schedule).

+--------------------+---------------------------------------------------------------------------+--------------------------------+----------+-----------+
| Name               | Description                                                               | Type                           | Required | Read-only |
+====================+===========================================================================+================================+==========+===========+
| ``id``             | Representing **Search Criteria** identifier.                              | ``guid``                       | yes      | yes       |
+--------------------+---------------------------------------------------------------------------+--------------------------------+----------+-----------+
| ``name``           | The label the criterion will be given in *QM*.                            | ``string(30)``                 | yes      | no        |
+--------------------+---------------------------------------------------------------------------+--------------------------------+----------+-----------+
| ``fieldName``      | The search field where is particular piece of information from e.g. date. | ``string(30)``                 | yes      | no        |
+--------------------+---------------------------------------------------------------------------+--------------------------------+----------+-----------+
| ``dataType``       | From the supported [Data Types](/v1/search-criteria#data-types).          | ``string``                     | yes      | no        |
+--------------------+---------------------------------------------------------------------------+--------------------------------+----------+-----------+
| ``conditionType``  | From the supported [Condition Types](/v1/search-criteria#data-types).     | ``string``                     | yes      | no        |
+--------------------+---------------------------------------------------------------------------+--------------------------------+----------+-----------+
| ``listOptions``    | Options collection of *key/values* for *List Data Type*.                  | ``dictionary(string, string)`` | no       | no        |
+--------------------+---------------------------------------------------------------------------+--------------------------------+----------+-----------+
| ``defaultValue``   | The ``listOptions`` default selected value.                               | ``string``                     | no       | no        |
+--------------------+---------------------------------------------------------------------------+--------------------------------+----------+-----------+

.. note::

  The **Search Criteria** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Search Criteria** properties are capitalized (eg. ``Id``, ``Name``,..)! \\


Data Type with Conditions Model
===============================

Represents the *Data Type* with its supported *Conditions* as model for lookup with available properties used for setting valid combination of ``dataType`` and ``conditionType`` for **Search Criteria**.

+--------------------+----------------------------------------------------------------------+-------------------------------+
| Name               | Description                                                          | Type                          |
+====================+======================================================================+===============================+
| ``dateType``       | The *Data Type* id and name.                                         | ``keyValue(byte, string)``    |
+--------------------+----------------------------------------------------------------------+-------------------------------+
| ``conditions``     | The *Data Type* supported *Conditions* as dictionary of id and name  | ``dictionary(byte, string)``  |
+--------------------+----------------------------------------------------------------------+-------------------------------+

.. note::

  | The **Data Type with Condition** properties names (*Name* column) is
  | for default usage by ``JSON``, for ``C# Wrapper`` usage the **Data Type**
  | with Condition** properties are capitalized (eg. ``Id``, ``Name``,..)!
  | There is metrics of available [Condition Types](/v1/search-criteria#data-types) for each [Data Type](/v1/search-criteria#data-types) see more in section ["Data type and Conditions combinations"](/v1/search-criteria#combination).

Data Types
^^^^^^^^^^

Boolean (or logical data type)
------------------------------

A value that is true, false or unknown, so filtered for, against or ignored.

DateTime
--------

The date and time

List
----

A list of options that may either be selected individually or in combination.

ListNumeric
-----------

A list of options that equate to a particular numerical value.

Numeric
-------

Fixed precision and scale numbers, functionally equivalent to decimal.

Textual
-------

A single character or string.

Time
----

The Time and no date.


Condition Types
^^^^^^^^^^^^^^^

Any
---

Enables the selection of a combination of values when used in conjunction with a list.

GreaterThan
-----------

All values greater than the chosen.

GreaterThanEqual
----------------

All values greater than or equal to the chosen.

LessThan
--------

All values less than the chosen.

LessThanEqual
-------------

All values less than or equal to the chosen.

Equal
-----

Only values equal to the chosen, in the case of a list presenting the user with a dropdown rather than a series of selection options.

NotEqual
--------

All values that do not equal the chosen.

Contains
--------

Includes the specified text.

NotContains
-----------

Does not include the specified text.

Range
-----

All values that exist within the chosen range.

StartsWith
----------

Values begin with specified characters.

EndsWith
--------

Values end with specified characters.


Data Types and Conditions Combinations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The table of supported **Conditions** for each **Data Type**.

+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| Condition / Data Type | Boolean  | DateTime | List     | ListNumeric | Numeric | Textual | Time  |
+=======================+==========+==========+==========+=============+=========+=========+=======+
| **Any**               |          |          | ✔        | ✔           |         |         |       |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **GreaterThan**       |          | ✔        |          |             | ✔       |         | ✔     |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **GreaterThanEqual**  |          | ✔        |          |             | ✔       |         | ✔     |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **LessThan**          |          | ✔        |          |             | ✔       |         | ✔     |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **LessThanEqual**     |          | ✔        |          |             | ✔       |         | ✔     |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **Equal**             | ✔        | ✔        | ✔        |  ✔          | ✔       | ✔       | ✔     |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **NotEqual**          | ✔        | ✔        |          |             | ✔       | ✔       | ✔     |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **Contains**          |          |          | ✔        |  ✔          |         | ✔       |       |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **NotContains**       |          |          |          |             |         | ✔       |       |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **Range**             |          | ✔        |          |             | ✔       |         | ✔     |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **StartsWith**        |          |          |          |             |         | ✔       |       |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
| **EndsWith**          |          |          |          |             |         | ✔       |       |
+-----------------------+----------+----------+----------+-------------+---------+---------+-------+
