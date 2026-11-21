LongDuration
============

Overview
--------

This test validates the long-duration reliability of the
DS.Iridium9603 subsystem.

-------------------------------------------------------------------------------

Purpose
-------

This test validates continuous operation of:

- Mobile Originated (MO) message transmission.
- Mobile Terminated (MT) message retrieval.
- Ring Alert unsolicited result code processing.
- Mobile Originated (MO) to Mobile Terminated (MT) text payload transfer.
- Mobile Originated (MO) to Mobile Terminated (MT) binary payload transfer.
- Verbose and numeric modem response modes are both supported.

-------------------------------------------------------------------------------

Procedure
---------

1. Start the DS.Iridium9603 subsystem.
2. Repeatedly transmit Mobile Originated (MO) messages.
3. Repeatedly retrieve Mobile Terminated (MT) messages.
4. Process Ring Alert unsolicited result codes.
5. Exercise Mobile Originated (MO) to Mobile Terminated (MT) text payload transfers.
6. Exercise Mobile Originated (MO) to Mobile Terminated (MT) binary payload transfers.
7. Alternate between verbose and numeric response modes.
8. Operate continuously for approximately 48 hours.
9. Shutdown the DS.Iridium9603 subsystem.

-------------------------------------------------------------------------------

Observed Behavior
-----------------

Mobile Originated (MO) messages were transmitted successfully.

Mobile Terminated (MT) messages were retrieved successfully.

Mobile Originated (MO) to Mobile Terminated (MT) text payload transfers
completed successfully.

Mobile Originated (MO) to Mobile Terminated (MT) binary payload transfers
completed successfully.

Verbose `SBDRING` and numeric `126` unsolicited result codes were
detected and processed successfully.

Message retrieval using `AT+SBDRT` and `AT+SBDRB` completed
successfully.

The subsystem remained connected throughout the test and shut down
cleanly without entering the faulted state.

Evidence for this test is contained in `Test.log`.

-------------------------------------------------------------------------------

Result
------

PASS

-------------------------------------------------------------------------------

Notes
-----

This validation was performed using a physical Iridium 9603 transceiver.

No unexpected subsystem behavior was observed during this validation.