.. _recording-evaluations-label:

=====================
Recording Evaluations
=====================

Returns collection of *Evaluations* for given *Recording* call Id.

Recording Evaluations List Model
================================

Represent the **Recording Evaluations** list model with available properties.

.. note::

  | The list model used only to list **Recording Evaluations** with *GET* (*GetAll*) method.
  | Note that list model can change by adding/removing properties depending what users of *Coach REST API* will need in future.


+--------------------+-----------------------------------------------------------------+----------------------+
| Name               | Description                                                     | Type                 |
+====================+=================================================================+======================+
| ``id``             | Representing **Evaluation** identifier.                         | ``guid``             |
+--------------------+-----------------------------------------------------------------+----------------------+
| ``reference``      | The **Evaluation** reference.                                   | ``string``           |
+--------------------+-----------------------------------------------------------------+----------------------+
| ``score``          | The **Evaluation** score.                                       | ``int (nullable)``   |
+--------------------+-----------------------------------------------------------------+----------------------+
| ``date``           | The date when the **Evaluation** took place.                    | ``datetime``         |
+--------------------+-----------------------------------------------------------------+----------------------+
| ``isCompleted``    | Whether the **Evaluation** is completed.                        | ``boolean``          |
+--------------------+-----------------------------------------------------------------+----------------------+
| ``isAutoFailed``   | Wheather the **Evaluation** has failed.                         | ``boolean``          |
+--------------------+-----------------------------------------------------------------+----------------------+
| ``comments``       | The **Evaluations** comments.                                   | ``string``           |
+--------------------+-----------------------------------------------------------------+----------------------+

.. note::

  The **Recording Evaluations** properties names (*Name* column) is for default usage by ``JSON``, for ``C# Wrapper`` usage the **Recording Evaluations** properties are capitalized (eg. ``Id``, ``Name``,..)!


List of Evaluations for Recording Call Id
=========================================

The list of **Recording Evaluations** for :ref:`current Tenant <tenant-label>`.

Default REST approach
^^^^^^^^^^^^^^^^^^^^^

    GET /api/v1/:tenantCode/recording-evaluations/:callId

Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``callId`` The **Recording** call id, a valid and non-empty ``string``.

.. danger::

  | Remember to remove ``/``, ``.``, ``:`` and ``\`` characters from ``callId`` string. If not the response will be 404 due to invalid URL.
  |
  | Remember to add *API Key* as *customer*key* and *API Secret* as *customer*secret* into your *Request HTTP Header*. See more in :ref:`getting-started-label`.


Return value
------------

* If there is no error: ``JSON`` array of :ref:`recording-evaluations-label`.
* If there is an error: ``JSON`` :ref:`client-error-label` object.

C# Wrapper approach
^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp
   :linenos:

   RecordingEvaluationWrapper(int tenantCode, string apiKey, string apiSecret).GetEvaluationsByCallId(string callId);


Parameters
----------

* ``tenantCode`` :ref:`Current Tenant <tenant-label>` code, a valid ``integer`` greater or equal to 1000.
* ``apiKey`` :ref:`Current Tenant <tenant-label>` API Key provided by **Qualtrak**.
* ``apiSecret`` :ref:`Current Tenant <tenant-label>`  API Secret provided by **Qualtrak**.
* ``callId`` The **Recording** call id, a valid and non-empty ``string``.

.. danger::

  Remember to remove ``/``, ``.``, ``:`` and ``\`` characters from ``callId`` string. If not the response will be 404 due to invalid URL.


Safe Call Id Extension Method
-----------------------------

Create the C# ``string`` Extension Method to make ``callId`` safe and call it always to make safe ``callId`` to get ``Evauluations``:

.. code-block:: csharp
   :linenos:

    public static class StringExtensions
    {
        public static string ToSafeCallId(this string callId)
        {
            string result = callId.Replace(@"\", "")
                                    .Replace("/", "")
                                    .Replace(".", "")
                                    .Replace(":", "");

            return result;
        }
    }

    // and call it as:
    string callId = "10.1.1.1:300/recording/2012/01/01/a.wav".ToSafeCallId();
    // callId => "10111300recording20120101awav"


Return value
------------

* If there is no error: ``ResaultContent<ICollection<RecordingEvaluationList>>.Result`` object collection of the :ref:`recording-evaluations-label`.
* If there is an error: ``ResaultContent<ICollection<RecordingEvaluationList>>.Error`` object. See more in :ref:`client-error-label`.

Example usage
-------------

.. code-block:: csharp
   :linenos:

   int tenantCode = 1000;
   string key = "ddZXdAZvWefFqxAEH62u";
   string secret = "wx6GiQggg9YRH89XT5aKoY2qZLVquYjxARtgZhuGoFQX5w6Lws";

   // Preffered way of creating ``callId`` by calling the ``string`` extension method ``ToSafeCallId``.
   // See implementation in "Safe Call Id Extension Method"!
   string callId = "10.1.1.1:300/recording/2012/01/01/a.wav".ToSafeCallId();

   // Another way but error prone!
   // string callId = "/10.1.1.1:300/recording/2012/01/01/a.wav".Replace("/", "").Replace(".", "").Replace(":", "");

   RecordingEvaluationWrapper recordingEvaluationWrapper = new RecordingEvaluationWrapper(tenantCode, key, secret);
   ResponseContent<ICollection<RecordingEvaluationList>> response = recordingEvaluationWrapper.GetEvaluationsByCallId(callId);

   if (response.Result != null)
   {
        // Use Result as requested Recording Evaluations for displaying.
        ICollection<RecordingEvaluationList> recordingEvaluations = response.Result;
   }
   else
   {
       // TODO: The error handling...
       Console.WriteLine(response.Error);
   }
