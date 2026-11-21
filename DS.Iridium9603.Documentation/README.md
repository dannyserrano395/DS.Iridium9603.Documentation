Iridium9603 README
==================

Overview
--------

The Iridium9603 subsystem provides an interface for communicating with
an Iridium 9603 satellite transceiver.

The subsystem manages command processing, unsolicited result code (URC)
processing, and managing lifecycle state.

The subsystem is designed for applications requiring reliable high-latency
satellite communications over the Iridium Short Burst Data (SBD).

-------------------------------------------------------------------------------

Features
--------

- Command processing.
- Unsolicited result code (URC) processing.
- Managing lifecycle state.

-------------------------------------------------------------------------------

Getting Started
---------------

Create an instance of the subsystem with the required options:

    var options = new Iridium9603Options
    {
        BaudRate = 19200,
        DataBits = 8,
        Parity = Parity.None,
        StopBits = StopBits.One,
        PortNames = ["COM3"]
    };

    var iridium9603 = new Iridium9603(options);

Connect the subsystem:

    await iridium9603.ConnectAsync();

Verify the subsystem is connected:

    var isConnected = iridium9603.IsConnected();

Execute a command:

    var response = await iridium9603.ExecuteCommandAsync("AT");

Process unsolicited result codes (URCs):

    await iridium9603.WaitForUnsolicitedResultCodeAsync();

    if (iridium9603.TryReadUnsolicitedResultCode(out var urc))
    {
        Console.WriteLine(urc.Result);
    }

Disconnect the subsystem:

    await iridium9603.DisconnectAsync();

Verify the subsystem is disconnected:

    var isDisconnected = iridium9603.IsDisconnected();

-------------------------------------------------------------------------------

Documentation
-------------

Additional documentation is available in the following files:

- Architecture.md
- Assumptions.md
- SupportedCommands.md
- Validation.md

-------------------------------------------------------------------------------

License
-------

Proprietary software.

All rights reserved.