Supported Commands
==================

Overview
--------

This test validates that the DS.Iridium9603 subsystem correctly executes
the supported Iridium 9603 command set.

The test validates command execution across all supported modem echo and
response mode combinations.

-------------------------------------------------------------------------------

Purpose
-------

This test verifies that:

- Supported Iridium 9603 commands can be executed through the subsystem.
- Supported commands operate correctly with command echo enabled and
  disabled.
- Supported commands operate correctly with verbose and numeric modem
  response modes.
- READY-state TEXT mode operations are correctly processed.
- READY-state BINARY mode operations are correctly processed.
- The subsystem remains operational while executing the supported command
  set.

-------------------------------------------------------------------------------

Procedure
---------

1. Start the DS.Iridium9603 subsystem.
2. Configure the modem for command echo enabled and verbose response mode:

       `ATE1`
       `ATV1`

3. Execute the supported Iridium 9603 command set.
4. Exercise READY-state TEXT and BINARY mode operations.
5. Configure the modem for command echo enabled and numeric response mode:

       `ATE1`
       `ATV0`

6. Execute the supported Iridium 9603 command set.
7. Exercise READY-state TEXT and BINARY mode operations.
8. Configure the modem for command echo disabled and verbose response mode:

       `ATE0`
       `ATV1`

9. Execute the supported Iridium 9603 command set.
10. Exercise READY-state TEXT and BINARY mode operations.
11. Configure the modem for command echo disabled and numeric response mode:

        `ATE0`
        `ATV0`

12. Execute the supported Iridium 9603 command set.
13. Exercise READY-state TEXT and BINARY mode operations.
14. Shutdown the DS.Iridium9603 subsystem.

-------------------------------------------------------------------------------

Observed Behavior
-----------------

All commands listed in `SupportedCommands.md` were successfully executed
against a physical Iridium 9603 satellite transceiver.

Each supported command was validated under the following modem
configurations:

- `ATE1` / `ATV1`
- `ATE1` / `ATV0`
- `ATE0` / `ATV1`
- `ATE0` / `ATV0`

READY-state TEXT mode operations were validated using both the
`AT+SBDWT=<text>` and `AT+SBDWT` command forms.

READY-state BINARY mode operations were validated using `AT+SBDWB`.

The subsystem correctly parsed echoed and non-echoed command responses,
as well as verbose (`OK`) and numeric (`0`) result codes.

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