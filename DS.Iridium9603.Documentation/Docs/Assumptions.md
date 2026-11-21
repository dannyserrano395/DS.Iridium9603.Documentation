Iridium9603 Assumptions
=======================

Overview
--------

This document describes the assumptions upon which the Iridium9603
subsystem is designed.

These assumptions are based on the Iridium ISU AT Command Reference
(MAN0009 Version 5) and observed Iridium 9603 modem behavior.

-------------------------------------------------------------------------------

Command Processing
------------------

The modem is assumed to process one command at a time.

While processing a command, the modem is assumed to reserve the serial
port until command processing completes.

-------------------------------------------------------------------------------

Unsolicited Result Code Processing
----------------------------------

The modem is assumed to reserve the serial port while processing a
command or operating in READY mode.

URCs are assumed to be delivered only after the modem releases ownership
of the serial port.

URCs are assumed not to be injected into the middle of command
responses or while the modem is operating in READY mode.