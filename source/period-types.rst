.. _period-types-label:

============================
Period Types and Occurrences
============================

Period Types
============

The **Period Types** are essential part of :ref:`schedule-label` and currently these **Period Types** are supported:

Daily
^^^^^

The :ref:`schedule-label` will run every day.

Weekly
^^^^^^

The :ref:`schedule-label` will run every week.

Monthly
^^^^^^^

The :ref:`schedule-label` will run every month.

Quarterly
^^^^^^^^^

The :ref:`schedule-label` will run quarterly or every three months.

Custom
^^^^^^

A custom form and to date for a one-off search. The ``customDateFrom`` and ``customDateTo`` dates must be set to cover a period prior to the :ref:`Schedule's <schedule-label>` ``startDate``.

Occurrences
===========

The **Occurrences** are part of **Period Types** describing the type of occurrence on specific **Period Type**. **Occurrences** are triggered by the  :ref:`Schedule's <schedule-label>` ``startDate``.

Currently supported **Occurrences** are:

None
^^^^

Used only for *Custom* **Period Type** since it will always have only one occurrence.

Infinite
^^^^^^^^

Will occur infinitely.

Number Of Times
^^^^^^^^^^^^^^^

Will occur for the specified number of times described through number declared :ref:`Schedule's <schedule-label>` ``occurrenceTimesNumber`` property.

Until End Date
^^^^^^^^^^^^^^

Will occur until some specified :ref:`Schedule's <schedule-label>` ``endDate`` that is higher or equal of ``startDate``.

Period Types and Occurrences Combinations
=========================================

The combination of **Period Types** and the supported **Occurrences** for **Period Type**.

+---------------------+----------+----------+-----------------+-----------------+
| Period \ Occurrence | None     | Infinite | Number Of Times | Until End Date  |
+=====================+==========+==========+=================+=================+
| **Daily**           |          | ✔        | ✔               | ✔               |
+---------------------+----------+----------+-----------------+-----------------+
| **Weekly**          |          | ✔        | ✔               | ✔               |
+---------------------+----------+----------+-----------------+-----------------+
| **Monthly**         |          | ✔        | ✔               | ✔               |
+---------------------+----------+----------+-----------------+-----------------+
| **Quarterly**       |          | ✔        | ✔               | ✔               |
+---------------------+----------+----------+-----------------+-----------------+
| **Custom**          | ✔        |          |                 |                 |
+---------------------+----------+----------+-----------------+-----------------+

Period Types and Occurrences with Required [Schedule](/v1/schedule) Model Properties
====================================================================================

The table of **Occurrences** with valid **Period Types** and required :ref:`schedule-label` model properties. Check mark denotes required :ref:`schedule-label`  model property for **Period Type** **Occurrence**.

+---------------------+------------------------------------------------------+---------------------------+--------------+----------------------+---------------------+
| Occurrences         | Period Type(s)                                       | ``occurrenceTimesNumber`` | ``endDate``  | ``customDateFrom``   | ``customDateTo``    |
+=====================+======================================================+===========================+==============+======================+=====================+
|                     |                                                      | :ref:`schedule-label` Model Properties                                                |
+---------------------+------------------------------------------------------+---------------------------+--------------+----------------------+---------------------+
| **None**            | **Custom**                                           |                           |              | ✔                    | ✔                   |
+---------------------+------------------------------------------------------+---------------------------+--------------+----------------------+---------------------+
| **Infinite**        | **Daily**, **Weekly**, **Monthly** and **Quarterly** |                           |              |                      |                     |
+---------------------+------------------------------------------------------+---------------------------+--------------+----------------------+---------------------+
| **Number Of Times** | **Daily**, **Weekly**, **Monthly** and **Quarterly** | ✔                         |              |                      |                     |
+---------------------+------------------------------------------------------+---------------------------+--------------+----------------------+---------------------+
| **Until End Date**  | **Daily**, **Weekly**, **Monthly** and **Quarterly** |                           | ✔            |                      |                     |
+---------------------+------------------------------------------------------+---------------------------+--------------+----------------------+---------------------+

.. danger::

  Beware that the *API* will raise an exception when not needed property is sent for some combination of **Period Type** and **Occurrence**. Eg. if for *Daily* **Period Type** as *Infinite* **Occurrence** is sent not needed ``endDate`` property, this will raise an exception with message: *"Daily period type of Infinite occurrence type cannot have an end date assigned to it!"*.
