Iridium9603 Architecture
========================

Overview
--------

This document describes the architecture of the Iridium9603 subsystem.

The Iridium9603 subsystem provides an interface for communicating with
an Iridium 9603 satellite transceiver.

The subsystem manages command processing, unsolicited result code (URC)
processing, and managing lifecycle state.

-------------------------------------------------------------------------------

High-Level Architecture
-----------------------

    +--------------------+
    |     Consumer       |
    +----------+---------+
               |
               v
    +--------------------+
    |    Iridium9603     |
    +----------+---------+
               |
               +------------------+
               |                  |
               v                  v
    +-----------------+    +--------------+
    | Command Handler |    | URC Listener |
    +-----------------+    +--------------+
               |                  |
               +--------+---------+
                        |
                        v
          +-----------------------+
          | SerialWindowTransport |
          +-----------------------+
                        |
                        v
                 +------------+
                 | Iridium9603|
                 |   Modem    |
                 +------------+

-------------------------------------------------------------------------------

Responsibilities
----------------

Iridium9603

The Iridium9603 class is the primary entry point into the subsystem.

Responsibilities include:

- Managing lifecycle state.
- Processing commands.
- Processing unsolicited result codes (URCs).
- Coordinating access to the modem.

SerialWindowTransport

The SerialWindowTransport class provides access to the serial interface
connected to the modem.

Responsibilities include:

- Sending data to the modem.
- Receiving data from the modem.
- Providing buffered access to received data.
- Enforcing read and write timeouts.

-------------------------------------------------------------------------------

Command Processing
------------------

Command processing is serialized through a SemaphoreSlim to ensure that
only one command is active at a time.

The command processing sequence is:

    Consumer
        ↓
    ExecuteCommandAsync(...)
        ↓
    Acquire Semaphore
        ↓
    Send Command
        ↓
    Read Response
        ↓
    Release Semaphore

If command processing fails while the subsystem is connected, the
subsystem transitions to the Faulted and Disconnected states.

-------------------------------------------------------------------------------

Unsolicited Result Code Processing
----------------------------------

A dedicated background task continuously monitors the modem for
unsolicited result codes (URCs).

The listener performs the following sequence:

    Wait For Data
        ↓
    Identify URC
        ↓
    Parse URC
        ↓
    Queue URC
        ↓
    Notify Consumer

URCs are placed into an internal channel for later processing by
consumers.

Consumers may:

    await WaitForUnsolicitedResultCodeAsync();
    TryReadUnsolicitedResultCode(...);

-------------------------------------------------------------------------------

Lifecycle States
----------------

The subsystem exposes three lifecycle states:

    Connected
    Faulted
    Disconnected

Each state is represented by a Task.

`Connected`

Completed when a connection to the Iridium 9603 modem is successfully
established.

Canceled when a connection attempt fails or the subsystem is disposed
before the Connected state is set.

`Faulted`

Faulted with the exception that caused the subsystem to transition to the
Faulted state.

Canceled when the subsystem successfully completes without faulting or
the subsystem is disposed before the Faulted state is set.

`Disconnected`

Completed when the subsystem is successfully disconnected from the
Iridium 9603 modem.

Completed when a fault occurs while the subsystem is connected.

Canceled when a connection attempt fails or the subsystem is disposed
before the Disconnected state is set.

-------------------------------------------------------------------------------

Fault Handling
--------------

If a connection attempt fails:

    Cancel Connected
        ↓
    Transition To Faulted
        ↓
    Cancel Disconnected

If a fault occurs while the subsystem is connected:

    Cancel Internal Operations
        ↓
    Transition To Faulted
        ↓
    Transition To Disconnected

Recovery is performed by creating a new Iridium9603 instance.

-------------------------------------------------------------------------------

Exceptions
----------

The subsystem uses a single internal exception type, Iridium9603Exception,
to represent subsystem-specific errors.

Each exception contains an Iridium9603ErrorCode identifying the error.

The following error codes are defined:

`None`

Indicates that no error is specified.

`ModemConnectionFailed`

Indicates that a connection attempt to the Iridium 9603 modem failed.

`CommandFailed`

Indicates that command processing failed.

`UnsolicitedResultCodeFailed`

Indicates that unsolicited result code (URC) processing failed.

`InvalidState`

Indicates that an operation was attempted from an invalid lifecycle state.

-------------------------------------------------------------------------------

Disposal
--------

The subsystem supports deterministic disposal of internal resources.

Consumers should dispose the subsystem only after the Connected,
Faulted, and Disconnected lifecycle states have completed or been
canceled.

Otherwise, the subsystem cancels any incomplete lifecycle states but
does not dispose the synchronization primitives. This prevents
synchronization primitives from being disposed while they may still be in
use. In this case, the synchronization primitives are reclaimed by the
garbage collector when the subsystem instance is no longer referenced.