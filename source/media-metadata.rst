.. _media-metadata-label:

===================
Media File Metadata
===================

The needed metadata to get :ref:`User (Agent) <user-label>` recorded media files from :ref:`recorder-label`.

Required Media File Metadata
============================

The currently supported and required metadata by *Coach* for getting media files from :ref:`recorder-label` for :ref:`User (Agent) <user-label>`.

RecordingID
^^^^^^^^^^^

The database field name for recorder media file identifier or id.

RecordingFileName
^^^^^^^^^^^^^^^^^

The database field name for the recorder media file name.

RecorderUserID
^^^^^^^^^^^^^^

The database field name for the recorder media file belonging user (agent).

Date
^^^^

The database field name for the recorder media file date time stamp.

.. note::

  | When the particular :ref:`recorder-label` is acquired by *REST API*, for ``mediaFileMetadataCollection``  will be sent as collection of this four instances of ``MediaPlayerMetadata``.
  | Then there is only need for setting matching [Recorder's](/v1/recorder) ``fieldName`` and its [Database Data Type](/v1/media-metadata#database-data-types).


Media File Metadata Model
=========================

Represents the **Media File Metadata** model as value object with available properties and its behaviors used for :ref:`recorder-label`.

+---------------------------+-----------------------------------------------------------------------------------------------------+----------------------+----------+-----------+
| Name                      | Description                                                                                         | Type                 | Required | Read-only |
+===========================+=====================================================================================================+======================+==========+===========+
| ``fieldName``             | The database field name to match the meaning of ``localFieldName``.                                 | ``string(64)``       | yes      | no        |
+---------------------------+-----------------------------------------------------------------------------------------------------+----------------------+----------+-----------+
| ``databaseDataType``      | The [database data type](/v1/media-metadata#database-data-types) for the db ``fieldName``.          | ``DatabaseDataType`` | yes      | no        |
+---------------------------+-----------------------------------------------------------------------------------------------------+----------------------+----------+-----------+
| ``localFieldName``        | *Coach* name for ``fieldName``.                                                                     | ``string``           | N/A      | yes       |
+---------------------------+-----------------------------------------------------------------------------------------------------+----------------------+----------+-----------+
| ``localDatabaseDataType`` | The *Coach* [database data type](/v1/media-metadata#database-data-types) for the db ``fieldName``.  | ``DatabaseDataType`` | N/A      | yes       |
+---------------------------+-----------------------------------------------------------------------------------------------------+----------------------+----------+-----------+

.. note::

  Note that lookup values for setting ``databaseDataType`` are part of [Recorder Domain Model](/v1/recorder#recorder-model).


Database Data Type Model
========================

Represents the supported *Database Data Type* as value object.

+--------------+-----------------------------------------------------------------------+-------------+----------+-----------+---------+
| Name         | Description                                                           | Type        | Required | Read-only | Default |
+==============+=======================================================================+=============+==========+===========+=========+
| ``id``       | The ``name`` as uppercase version.                                    | ``string``  | N/A      | yes       |         |
+--------------+-----------------------------------------------------------------------+-------------+----------+-----------+---------+
| ``name``     | The database data type name.                                          | ``string``  | N/A      | yes       |         |
+--------------+-----------------------------------------------------------------------+-------------+----------+-----------+---------+
| ``length``   | The database data type length, applicable only to string/char values. | ``integer`` | no       | no        | ``0``   |
+--------------+-----------------------------------------------------------------------+-------------+----------+-----------+---------+

.. note::

  Note that only the length can be changed the ``id`` and ``name`` are fixed values!


Database Data Types
^^^^^^^^^^^^^^^^^^^

The supported database data types are:

* **Integer**
* **NVarchar** (overrides default length to 255)
* **Varchar**  (overrides default length to 255)
* **Bit**
* **Datetime**
