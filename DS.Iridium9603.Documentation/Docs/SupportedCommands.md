
Supported Commands
==================

Overview
--------

This document lists the AT commands and unsolicited result codes (URCs)
supported by the Iridium9603 subsystem.

-------------------------------------------------------------------------------

Supported AT Commands
---------------------

### General

- `AT`
- `ATE`
- `ATE0`
- `ATE1`
- `ATQ`
- `ATQ0`
- `ATV`
- `ATV0`
- `ATV1`
- `ATZ`
- `ATZ0`
- `ATZ1`
- `AT&F`
- `AT&F0`
- `AT&K`
- `AT&K0`
- `AT&K3`
- `AT*F`
- `AT*R0`
- `AT*R1`
- `AT&D`
- `AT&D0`
- `AT&D1`
- `AT&D2`
- `AT&D3`
- `AT&W`
- `AT&W0`
- `AT&W1`
- `AT&Y`
- `AT&Y0`
- `AT&Y1`

-------------------------------------------------------------------------------

### Identification

- `ATI`
- `ATI0`
- `ATI1`
- `ATI2`
- `ATI3`
- `ATI4`
- `ATI5`
- `ATI6`
- `ATI7`
- `AT+CGMI`
- `AT+CGMM`
- `AT+CGMR`
- `AT+CGSN`
- `AT+GMI`
- `AT+GMM`
- `AT+GMR`
- `AT+GSN`

-------------------------------------------------------------------------------

### Clock

- `AT+CCLK?`

-------------------------------------------------------------------------------

### Configuration

- `AT&V`
- `AT+CIER=?`
- `AT+CIER=`
- `AT+CIER?`
- `AT+IPR=`
- `AT+IPR=?`
- `AT+IPR?`
- `AT+SBDMTA=`
- `AT+SBDMTA?`
- `AT+SBDMTA=?`
- `AT+SBDAREG=`
- `AT+SBDAREG?`
- `AT+SBDAREG=?`
- `AT+SBDREG=`
- `AT+SBDREG?`
- `AT+SBDDSC=`
- `AT+SBDDSC?`
- `AT+SBDST=`
- `AT+SBDST?`
- `AT+CULK?`

-------------------------------------------------------------------------------

### Signal and Status

- `AT+CSQ`
- `AT+CSQ=?`
- `AT+CSQF`
- `AT+CRIS`
- `AT+CRISX`
- `AT-MSGEO`
- `AT-MSGEOS`
- `AT-MSSTM`
- `AT%R`

-------------------------------------------------------------------------------

### Short Burst Data (SBD)

#### Mobile-Originated Buffer

- `AT+SBDWT`
- `AT+SBDWT=`
- `AT+SBDWB=`

#### Mobile-Terminated Buffer

- `AT+SBDRB`
- `AT+SBDRT`

#### Session Management

- `AT+SBDI`
- `AT+SBDIX`
- `AT+SBDIX=`
- `AT+SBDIXA`
- `AT+SBDIXA=`
- `AT+SBDDET`

#### Mailbox Management

- `AT+SBDD0`
- `AT+SBDD1`
- `AT+SBDD2`

#### Status

- `AT+SBDS`
- `AT+SBDSX`
- `AT+SBDLOE`

#### Gateway

- `AT+SBDGW`
- `AT+SBDGWN`

#### Registration

- `AT+SBDC`
- `AT+SBDTC`

-------------------------------------------------------------------------------

### S-Registers

- `ATS3`
- `ATS3?`
- `ATS3=`
- `ATS4`
- `ATS4?`
- `ATS4=`
- `ATS5`
- `ATS5?`
- `ATS5=`
- `ATS13`
- `ATS13?`
- `ATS13=`
- `ATS14`
- `ATS14?`
- `ATS14=`
- `ATS21`
- `ATS21?`
- `ATS21=`
- `ATS23`
- `ATS23?`
- `ATS23=`
- `ATS39`
- `ATS39?`
- `ATS39=`
- `ATS112`
- `ATS112?`
- `ATS112=`
- `ATS113`
- `ATS113?`
- `ATS113=`
- `ATS121`
- `ATS121?`
- `ATS121=`
- `ATS122`
- `ATS122?`
- `ATS122=`

-------------------------------------------------------------------------------

Supported Unsolicited Result Codes (URCs)
-----------------------------------------

The Iridium9603 subsystem currently supports the following unsolicited
result codes (URCs):

### Ring Alert

- Verbose: `SBDRING`
- Numeric: `126`

### Indicator Event

- `+CIEV:<indicator>,<value>`

### Automatic Registration Event

- `+AREG:<event>,<registration error>`

-------------------------------------------------------------------------------

Notes
-----

- Commands are executed asynchronously.
- Command execution is thread-safe.
- Only one command is executed by the modem at a time.
- URCs are processed asynchronously by a dedicated background listener.
- Both verbose and numeric modem response modes are supported.
- Where supported by the Iridium 9603 firmware, shorthand command forms
  (for example `ATE`, `ATQ`, `ATV`, `ATZ`, `AT&F`, `AT&K`, `AT&W`,
  `AT&Y`, `AT&D`, and `ATI`) are accepted and are equivalent to their
  default numeric form (for example `ATE0`, `ATQ0`, `ATV0`, `ATZ0`,
  `AT&F0`, `AT&K0`, `AT&W0`, `AT&Y0`, `AT&D0`, and `ATI0`).
- Supported commands have been validated against a physical Iridium 9603
  satellite transceiver.
