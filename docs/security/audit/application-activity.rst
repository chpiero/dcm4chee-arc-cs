Application Activity
====================

Trigger Events
--------------
This audit message is emitted when the archive is started or stopped using the archive user interface. It is also
emitted during archive startup or shutdown.

Message Structure
-----------------

.. csv-table:: Entities in Application Activity Audit Message

    :ref:`event-identification-application-activity`
    :ref:`active-participant-archive-application-activity`
    :ref:`active-participant-user-application-activity`, Present only if triggered using Archive UI
    :ref:`audit-general-message-audit-source`

.. csv-table:: Event Identification
   :name: event-identification-application-activity
   :widths: 30, 5, 65
   :header: Field Name, Opt, Description

   EventID, M, "| EV (110100, DCM, 'Application Activity')"
   EventActionCode, M, | Execute ⇒ 'E'
   EventDateTime, M, | The time at which the event occurred
   EventOutcomeIndicator, M, | Success ⇒ '0'
   EventTypeCode, M, "| DT (110120, DCM, 'Application Start')
   | DT (110121, DCM, 'Application Stop')"

.. csv-table:: Active Participant : Archive
   :name: active-participant-archive-application-activity
   :widths: 30, 5, 65
   :header: Field Name, Opt, Description

   UserID, M, | Application entity titles of Archive Device as ; separated values
   UserIDTypeCode, U, "| Application startup/shutdown or archive deploy/undeploy ⇒ EV (113877, DCM, 'Device Name')
   | Triggered from UI ⇒ EV (12, RFC-3881, 'URI')"
   UserTypeCode, U, | Application ⇒ '2'
   AlternativeUserID, MC, | Process ID of Audit logger
   UserIsRequestor, M, | false
   RoleIDCode, M, "| EV (110150, DCM, 'Application')"
   NetworkAccessPointID, U, | Hostname/IP Address of the connection referenced by Audit logger
   NetworkAccessPointTypeCode, U, "| NetworkAccessPointID is host name ⇒ '1'
   | NetworkAccessPointID is an IP address ⇒ '2'"

.. csv-table:: Active Participant : User
   :name: active-participant-user-application-activity
   :widths: 30, 5, 65
   :header: Field Name, Opt, Description

   UserID, M, "| Secured version of archive ⇒ 'Logged in User name'
   | Unsecured version of archive ⇒ 'Remote IP address'"
   UserIDTypeCode, U, "| Secured Archive ⇒ EV (113871, DCM, 'Person ID')
   | Unsecured Archive ⇒ EV (110182, DCM, 'Node ID')"
   UserTypeCode, U, | Person ⇒ '1'
   UserIsRequestor, M, | true
   RoleIDCode, M, "| EV (110151, DCM, 'ApplicationLauncher')"
   NetworkAccessPointID, U, | Hostname/IP Address of calling host
   NetworkAccessPointTypeCode, U, "| NetworkAccessPointID is host name ⇒ '1'
   | NetworkAccessPointID is an IP address ⇒ '2'"

Sample Message
--------------

.. code-block:: xml

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <AuditMessage xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="http://www.dcm4che.org/DICOM/audit-message.rnc">

        <EventIdentification EventActionCode="E" EventDateTime="2017-07-10T10:30:17.651+02:00" EventOutcomeIndicator="0">
            <EventID csd-code="110100" codeSystemName="DCM" originalText="Application Activity"/>
            <EventTypeCode csd-code="110120" codeSystemName="DCM" originalText="Application Start"/>
        </EventIdentification>

        <ActiveParticipant UserID="dcm4chee-arc" UserTypeCode="2" AlternativeUserID="5289" UserIsRequestor="false" NetworkAccessPointID="localhost" NetworkAccessPointTypeCode="1">
            <RoleIDCode csd-code="110150" codeSystemName="DCM" originalText="Application"/>
            <UserIDTypeCode csd-code="113877" codeSystemName="DCM" originalText="Device Name"/>
        </ActiveParticipant>

        <AuditSourceIdentification AuditSourceID="dcm4chee-arc">
            <AuditSourceTypeCode csd-code="4"/>
        </AuditSourceIdentification>

    </AuditMessage>