Indicator Events
================

Overview
--------

This test validates that the DS.Iridium9603 subsystem correctly detects,
parses, queues, and exposes indicator events.

-------------------------------------------------------------------------------

Purpose
-------

This test verifies that:

- Indicator events are detected by the background URC listener.
- Detected indicator events are correctly parsed and queued.
- Queued indicator events are exposed to consumers through the public API
  in FIFO order.
- Indicator event reporting can be enabled and disabled using `AT+CIER=`.
- Verbose and numeric modem response modes are both supported.

-------------------------------------------------------------------------------

Procedure
---------

1. Start the DS.Iridium9603 subsystem.
2. Configure the modem for either verbose (`ATV1`) or numeric (`ATV0`)
   response mode.
3. Enable indicator event reporting using:

       `AT+CIER=1,1,1,1,1`

4. Allow the modem to generate indicator events.
5. Verify queued URCs using:

       `--urc-count`

6. Read queued URCs using:

       `--try-urc`

7. Disable indicator event reporting using:

       `AT+CIER=0,0,0,0,0`

8. Verify no additional indicator events are queued.

9. Shutdown the DS.Iridium9603 subsystem.

-------------------------------------------------------------------------------

Observed Behavior
-----------------

The following indicator events were observed during validation:

Indicator 0

- `+CIEV:0,0`
- `+CIEV:0,1`
- `+CIEV:0,2`
- `+CIEV:0,3`
- `+CIEV:0,4`
- `+CIEV:0,5`

Indicator 1

- `+CIEV:1,0`
- `+CIEV:1,1`

Indicator 2

- `+CIEV:2,0`

Indicator 3

- Multiple `+CIEV:3,...` indicator events containing modem and location
  information were continuously received throughout the validation.

Indicator event reporting was successfully enabled and disabled using
`AT+CIER=`.

Queued indicator events were successfully retrieved in FIFO order
through the subsystem using `TryReadUnsolicitedResultCode()`.

`GetUnsolicitedResultCodeCount()` accurately reflected the number of
queued URCs throughout the validation.

Verbose `+CIEV` indicator events were detected and queued by the subsystem.

Numeric `+CIEV` indicator events were detected and queued by the subsystem.

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