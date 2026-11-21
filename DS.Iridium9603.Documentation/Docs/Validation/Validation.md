Validation
==========

Overview
--------

This document summarizes the validation performed for the
DS.Iridium9603 subsystem.

-------------------------------------------------------------------------------

Validation Environment
----------------------

Hardware

- Iridium 9603 satellite transceiver

Software

- DS.Iridium9603 subsystem
- DS.Iridium9603.CommandLine

Reference Documentation

- Iridium ISU AT Command Reference (MAN0009 Version 5)

-------------------------------------------------------------------------------

Command Validation
------------------

The following has been validated:

- Commands execute asynchronously.
- One command is executed at a time.
- Command execution is thread-safe.
- Command processing failures transition the subsystem to the Faulted
  and Disconnected states.

Result
------

PASS

-------------------------------------------------------------------------------

Lifecycle Validation
--------------------

The following has been validated:

- Connected completes after a successful connection.
- If a connection attempt fails, Connected and Disconnected are
  canceled, and Faulted faults with the exception that caused the
  connection failure.
- Faulted faults with the exception that caused the subsystem to fail.
- Disconnected completes after a successful disconnect or when a fault
  occurs while the subsystem is connected.
- Command and URC processing failures transition the subsystem to the
  Faulted and Disconnected state.
- Connected, Faulted, and Disconnected transition to the Canceled state
  when the subsystem is canceled before entering a lifecycle state.
- Calling `Dispose` cancels any lifecycle state that has not already
  transitioned to a terminal state.
- Lifecycle transitions are terminal.

Result
------

PASS

-------------------------------------------------------------------------------

Ring Alert Validation
---------------------

The following has been validated:

- Ring alerts are detected by the background URC listener.
- Ring alerts are queued for consumer processing.
- Ring alerts do not interfere with command execution.

The following ring alerts were observed:

- `SBDRING`
- `126`

Result
------

PASS

-------------------------------------------------------------------------------

+CIEV Validation
----------------

The following has been validated:

- `+CIEV` URCs are detected by the background URC listener.
- `+CIEV` URCs are queued for consumer processing.
- Indicator events do not interfere with command execution.

The following indicator events were observed:

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
- `+CIEV:2,1`

Indicator 3

- `+CIEV:3,<sv_id>,<beam_id>,<sv_bm>,<x>,<y>,<z>`

Result
------

PASS

-------------------------------------------------------------------------------

+AREG Validation
----------------

The following has been validated:

- `+AREG` URCs are detected by the background URC listener.
- `+AREG` URCs are queued for consumer processing.
- Automatic registration events do not interfere with command execution.

The following automatic registration events were observed:

- `+AREG:3,0`

Result
------

PASS