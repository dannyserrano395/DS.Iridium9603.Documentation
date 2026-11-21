Automatic Registration
======================

Overview
--------

This test validates that the DS.Iridium9603 subsystem correctly detects,
parses, queues, and exposes automatic registration events.

-------------------------------------------------------------------------------

Purpose
-------

This test verifies that:

- Automatic registration events are detected by the background URC 
  listener.
- Detected automatic registration events are correctly parsed and queued.
- Queued automatic registration events are exposed to consumers through
  the public API in FIFO order.
- `AT+SBDAREG=3` successfully enables automatic registration event
  reporting.
- Verbose and numeric modem response modes are both supported.

-------------------------------------------------------------------------------

Procedure
---------

1. Start the DS.Iridium9603 subsystem.
2. Configure the modem for either verbose (`ATV1`) or numeric (`ATV0`)
   response mode.
3. Enable automatic registration event reporting using:

       `AT+SBDAREG=3`

4. Allow the modem to perform an automatic registration.
5. Verify queued URCs using:

       `--urc-count`

6. Read queued URCs using:

       `--try-urc`

7. Shutdown the DS.Iridium9603 subsystem.

-------------------------------------------------------------------------------

Observed Behavior
-----------------

`AT+SBDAREG=3` successfully enabled automatic registration event
reporting.

The following unsolicited result code was observed:

- `+AREG:3,0`

The queued registration event was successfully retrieved through the
subsystem using `TryReadUnsolicitedResultCode()`.

`GetUnsolicitedResultCodeCount()` accurately reflected the number of
queued URCs throughout the validation.

Verbose `+AREG` indicator events were detected and queued by the subsystem.

Numeric `+AREG` indicator events were detected and queued by the subsystem.

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