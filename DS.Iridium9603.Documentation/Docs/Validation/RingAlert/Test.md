Ring Alerts
===========

Overview
--------

This test validates that the DS.Iridium9603 subsystem correctly detects,
parses, queues, and exposes ring alerts.

-------------------------------------------------------------------------------

Purpose
-------

This test verifies that:

- Ring alerts are detected by the background URC listener.
- Detected ring alerts are correctly parsed and queued.
- Queued ring alerts are exposed to consumers through the public API in
  FIFO order.
- Verbose and numeric modem response modes are both supported.

-------------------------------------------------------------------------------

Procedure
---------

1. Start the DS.Iridium9603 subsystem.
2. Configure the modem for either verbose (`ATV1`) or numeric (`ATV0`)
   response mode. 
3. Execute SBD session command using:

       `AT+SBDIX`

4. Allow the modem to receive ring alerts.
5. Verify queued URCs using:

       `--urc-count`

6. Read queued ring alerts using:

       `--try-urc`

7. Shutdown the DS.Iridium9603 subsystem.

-------------------------------------------------------------------------------

Observed Behavior
-----------------

The following ring alerts were observed during validation:

- `SBDRING`
- `126`

Queued ring alerts were successfully retrieved in FIFO order
through the subsystem using `TryReadUnsolicitedResultCode()`.

`GetUnsolicitedResultCodeCount()` accurately reflected the number of
queued URCs throughout the validation.

Verbose `SBDRING` ring alerts were detected and queued by the subsystem.

Numeric `126` ring alerts were detected and queued by the subsystem.

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