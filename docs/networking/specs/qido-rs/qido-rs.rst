QIDO-RS Specifications
^^^^^^^^^^^^^^^^^^^^^^

.. _qido-rs-search-for-studies:

QIDO-RS Search For Studies
""""""""""""""""""""""""""

.. csv-table:: QIDO-RS Search for Studies Specification
   :header: "Parameter", "Restrictions"

   "Media Types", "Restricted to 'multipart/related; type=application/dicom+xml' or 'application/json'"
   "Matching Attributes", "Refer :ref:`StudyAttributesMatching`"
   "Return Attributes", "Refer :ref:`StudyAttributesMatching`"
   "Limit and Offset supported", "Yes"
   "Person Name Matching", "Refer Person Name Matching Note"

.. csv-table:: QIDO-RS Study Attribute Matching
   :name: StudyAttributesMatching
   :header: "Attributes Names", "Tag", "Query Keys Matching (SCP)", "Return Attributes (SCP)"
   :file: study-attribute-matching.csv

Types of Matching :

1. "S" indicates the identifier attribute uses Single Value Matching.
2. "L" indicates UID List Matching.
3. "U" indicates Universal Matching. (Note : If only Universal Matching is supported for an attribute then that attribute can only be passed as an "includefield" query key.)
4. "*" indicates wild card matching.
5. "R" indicates Range Matching.
6. "SEQUENCE" indicates Sequence Matching.
7. "NONE" indicates that no matching is supported, but that values for this Element requested will be returned with all requests.
8. "UNIQUE" indicates that this is the Unique Key for that query level, in which case Universal Matching or Single Value Matching is used depending on the query level.

.. _qido-rs-search-for-series:

QIDO-RS Search For Series
"""""""""""""""""""""""""

.. csv-table:: QIDO-RS Search for Series Specification
   :header: "Parameter", "Restrictions"

   "Media Types", "Restricted to 'multipart/related; type=application/dicom+xml' or 'application/json'"
   "Matching Attributes", "Refer :ref:`StudyAttributesMatching` and :ref:`SeriesAttributesMatching`"
   "Return Attributes", "Refer :ref:`SeriesAttributesMatching`"
   "Limit and Offset supported", "Yes"
   "Relational Queries Supported", "Yes"
   "Person Name Matching", "Refer Person Name Matching Note"

Types of Matching: As explained above in QIDO-RS Search For Studies

.. csv-table:: QIDO-RS Series Attribute Matching
   :name: SeriesAttributesMatching
   :header: "Attributes Names", "Tag", "Query Keys Matching (SCP)", "Return Attributes (SCP)"
   :file: series-attribute-matching.csv

.. _qido-rs-search-for-instances:

QIDO-RS Search For Instances
""""""""""""""""""""""""""""

.. csv-table:: QIDO-RS Search for Instances Specification
   :header: "Parameter", "Restrictions"

   "Media Types", "Restricted to 'multipart/related; type=application/dicom+xml' or 'application/json'"
   "Matching Attributes", "Refer :ref:`StudyAttributesMatching`, :ref:`SeriesAttributesMatching` and :ref:`InstanceAttributesMatching`"
   "Return Attributes", "Refer :ref:`InstanceAttributesMatching`"
   "Limit and Offset supported", "Yes"
   "Relational Queries Supported", "Yes"
   "Person Name Matching", "Refer Person Name Matching Note"

Types of Matching: As explained above in QIDO-RS Search For Studies

.. csv-table:: QIDO-RS Instance Attribute Matching
   :name: InstanceAttributesMatching
   :header: "Attributes Names", "Tag", "Query Keys Matching (SCP)", "Return Attributes (SCP)"
   :file: instance-attribute-matching.csv

.. _qido-rs-search-for-patients:

QIDO-RS Search For Patients
"""""""""""""""""""""""""""

.. csv-table:: QIDO-RS Search for Patients Specification
   :header: "Parameter", "Restrictions"

   "Media Types", "Restricted to 'multipart/related; type=application/dicom+xml' or 'application/json'"
   "Matching Attributes", "Refer :ref:`PatientAttributesMatching`"
   "Return Attributes", "Refer :ref:`PatientAttributesMatching`"
   "Limit and Offset supported", "Yes"
   "Relational Queries Supported", "No"
   "Person Name Matching", "Refer Person Name Matching Note"

Types of Matching: As explained above in QIDO-RS Search For Studies

.. csv-table:: QIDO-RS Patient Attribute Matching
   :name: PatientAttributesMatching
   :header: "Attributes Names", "Tag", "Query Keys Matching (SCP)", "Return Attributes (SCP)"
   :file: patient-attribute-matching.csv


Person Name Matching Note :

- DCM4CHEE-QIDO-SERVICE supports "fuzzymatching" only for attributes having value representation as PN. If all characters
  of Person Name are in upper case, then the service performs case insensitive matching, else it shall perform case
  sensitive matching. The service also supports literal and wild card matching. It will not perform other forms of fuzzy matching.
  This applies to the following attributes:

   +--------------------------------------+------------------------------------------+
   | In :ref:`StudyAttributesMatching`    | Referring Physician's Name (0008,0090).  |
   +--------------------------------------+------------------------------------------+
   |                                      | Patient's Name (0010,0010).              |
   +--------------------------------------+------------------------------------------+
   |                                      | Physicians of Record (0008,1048).        |
   +--------------------------------------+------------------------------------------+
   | In :ref:`SeriesAttributesMatching`   | Performing Physician's Name (0008,1050). |
   +--------------------------------------+------------------------------------------+
   | In :ref:`InstanceAttributesMatching` | Verifying Observer Name (0040,A075).     |
   +--------------------------------------+------------------------------------------+
   | In :ref:`PatientAttributesMatching`  | Patient's Name (0010,0010).              |
   +--------------------------------------+------------------------------------------+

.. _qido-rs-connection-policies:

QIDO-RS Connection Policies
"""""""""""""""""""""""""""

.. _qido-rs-general:

General
'''''''
All standard RS connection policies apply. There are no extensions for RS options.

.. _qido-rs-number-of-connections:

Number Of Connections
'''''''''''''''''''''
The maximal number of simultaneous HTTP Requests is configurable. It is unlimited by default.

.. csv-table:: Number of HTTP Requests Supported

   "Maximum number of simultaneous HTTP requests", "No Maximum Limit (Configurable)"

.. _qido-rs-response-status:

Response Status
'''''''''''''''
DCM4CHEE-QIDO-SERVICE shall provide a response message header containing the appropriate status code indicating success, warning, or failure as shown below

.. csv-table:: HTTP Standard Response Codes
   :header: "Code", "Name", "Description"
   :file: http-standard-response-codes.csv


Web Service Endpoint URL
''''''''''''''''''''''''

*http://localhost:8080/dcm4chee-arc/aets/{AETitle}/rs*

Replace *{AETitle}* in the URL with the configured AE title.
