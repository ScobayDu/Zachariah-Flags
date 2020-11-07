<img src="https://t3.rbxcdn.com/6aa9c40c74df203ef4aa8449853b48a0" alt="Starboard Studios" height="50" />
<h3>Starboard Studios</h3>
<b>Zachariah Reborn - Fast Flags</b>

## Information
We use a "flags system" as part of our development process. When we release an update, not all of the code in it is necessarily active. Some of it is disabled by flags we remotely control without requiring you to manually run an update. This allows us to release and debug faster, and also allows us to revert changes if they turn out to be problematic.

## Types of Fast Flags

**Fast Flags (FFlag):** <br/> Regular Fast Flags are retrieved on startup and do not change unless Zachariah is shutdown and restarted.

**Dynamic Fast Flags (DFFlag):** <br/> Dynamic Fast Flags are retrieved every 30 seconds and can be changed at any moment in time.

**Synced Fast Flags (SFFlag):** <br/> Synced Fast Flags are synchronized between the client and the server.
They are retrieved at startup. The client uses whatever value the server has at the time.

**Dynamic Synced Fast Flags (DSFFlag):** <br/> Dynamic Synced Flags are retrieved every 30 seconds, which can be changed at any time. The client will use whatever value the server has. If this value is updated, the server will notify the client of the new updated value.

## Format

    04 bytes: Length of FFlags (in # of values, 0 for 'not passed')
    04 bytes: Length of DFFlags (in # of values, 0 for 'not passed')
    04 bytes: Length of SFFlags (in # of values, 0 for 'not passed')
    04 bytes: Length of DSFFlags (in # of values, 0 for 'not passed')
    Remainder: Data

## Flag Format

    01 bytes: Length of the name
    01 bytes: Type
        00 - Int08 + 1 byte
        01 - Int16 + 2 bytes
        02 - Int32 + 4 bytes
        03 - String + 1 byte for length, + nBytes
        04 - LogType + 1 byte
        05 - Double + 8 bytes
        06 - Boolean False + 0 bytes
        07 - Boolean True + 0 bytes
        08 - Array + 2 bytes for length, followed by each list item in the format [1B - Length][nB - Data]
        09 - Table + 2 bytes for length, followed by each item in the format [1B - Length][1B - Name Length][nB - Name][nB - Data]

The name and string bytes are passed through a bitwise NOT to make them less apparent in the overall data stream, but no strong encryption/complicated encoding is required on this.

## File Extentions

.bin <-- Used for network transfer and decoding efficiency. This is the default format for fast flags.

.json <-- The raw file information for public information and used for software that does not support our custom binary format.
