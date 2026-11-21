Flow Control
============

Overview
--------

This test validates the behavior of the DS.Iridium9603 subsystem with
RTS/CTS flow control enabled and disabled.

-------------------------------------------------------------------------------

Purpose
-------

This test verifies that:

- `AT&K3` enables RTS/CTS flow control.
- Ordinary AT commands continue to execute while RTS/CTS flow control is
  enabled.
- SBD operations that require data transfer or READY-state processing do
  not return their expected output when RTS/CTS flow control is enabled.
- Command timeouts caused by the incompatible flow-control configuration
  transition the subsystem to the Faulted and Disconnected states.
- `AT&K0` disables RTS/CTS flow control.
- The affected SBD operations complete successfully after RTS/CTS flow control
  is disabled.

-------------------------------------------------------------------------------

Procedure
---------

1. Start the DS.Iridium9603 subsystem.
2. Enable RTS/CTS flow control using:

       `AT&K3`

3. Execute ordinary supported AT commands and confirm that command
   execution remains operational.
4. Execute the READY-state TEXT mode command:

       `AT+SBDWT`

5. Record the subsystem lifecycle state after the command fails to return
   the expected output.
6. Create a new DS.Iridium9603 subsystem instance.
7. Execute the READY-state BINARY mode command:

       `AT+SBDWB=5`

8. Record the subsystem lifecycle state after the command fails to
    return the expected output.
9. Create a new DS.Iridium9603 subsystem instance.
10. Execute the text buffer read command:

        `AT+SBDRT`

11. Record the subsystem lifecycle state after the command fails to
    return the expected output.
12. Create a new DS.Iridium9603 subsystem instance.
13. Execute the binary buffer read command:

        `AT+SBDRB`

14. Record the subsystem lifecycle state after the command fails to
    return the expected output.
15. Create a new DS.Iridium9603 subsystem instance.
16. Disable flow control using:

        `AT&K0`

17. Execute the READY-state TEXT mode command:

        `AT+SBDWT`

18. Supply a TEXT value and verify that READY-state processing
    completes.
19. Copy the mobile-originated buffer to the mobile-terminated buffer
    using:

        `AT+SBDTC`

20. Read the TEXT value using:

        `AT+SBDRT`

21. Execute the READY-state BINARY mode command:

        `AT+SBDWB=`

22. Supply a five-byte BINARY value and verify that READY-state
    processing completes.
23. Copy the mobile-originated buffer to the mobile-terminated buffer
    using:

        `AT+SBDTC`

24. Read the BINARY value using:

        `AT+SBDRB`

25. Shutdown the DS.Iridium9603 subsystem.

-------------------------------------------------------------------------------

Observed Behavior
-----------------

Ordinary supported AT commands continued to execute successfully while
RTS/CTS flow control was enabled.

The inline TEXT buffer command `AT+SBDWT=` also executed successfully
while `AT&K3` was enabled.

The READY-state TEXT mode command `AT+SBDWT` did not return the expected
`READY` response while `AT&K3` was enabled. The command timed out, and the
connected subsystem transitioned to the Faulted and Disconnected states.

The READY-state BINARY mode command `AT+SBDWB=` did not return the
expected `READY` response while `AT&K3` was enabled. The command timed
out, and the connected subsystem transitioned to the Faulted and
Disconnected states.

The TEXT buffer read command `AT+SBDRT` did not return the expected
output while `AT&K3` was enabled. The command timed out, and the
connected subsystem transitioned to the Faulted and Disconnected states.

The BINARY buffer read command `AT+SBDRB` did not return the expected
output while `AT&K3` was enabled. The command timed out, and the
connected subsystem transitioned to the Faulted and Disconnected states.

A new subsystem instance was created, and RTS/CTS flow control was
disabled using `AT&K0`.

After `AT&K0`, `AT+SBDWT` returned `READY`. The supplied TEXT value was
accepted, copied to the mobile-terminated buffer, and successfully read
using `AT+SBDRT`.

After `AT&K0`, `AT+SBDWB=5` returned `READY`. The supplied BINARY value
was accepted, copied to the mobile-terminated buffer, and successfully
read using `AT+SBDRB`.

Evidence for this test is contained in `Test.log`.

-------------------------------------------------------------------------------

Result
------

PASS

-------------------------------------------------------------------------------

Notes
-----

This validation was performed using a physical Iridium 9603 transceiver.

No unexpected subsystem behavior was observed after the required
RTS/CTS flow-control configuration was identified.