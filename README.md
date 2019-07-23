# RaspberryPi Management Hat
Set of system scripts (and schematics itself) for managing hat board, used for safe shutdown, indicating system health, etc

## What is a Management Hat?
"Management hat" (RPMH hereafter) is hat (extension board), designed primary for Raspberry Pi 3 and Raspberry Pi Zero connectors.
It intended to provide the next hardware capabilities.
- Boot from powerdown state and safe shutdown button
- Safe warm restart button
- BOOT_OK LED
- Heartbeat LED
- Overheat LED
- "Shutdown initiated" LED
- "IP Link established" LED
- "TOR Link established" LED as special requirement for my own ["Tor anonymizing Wi-Fi hotspot" project](https://tor-assets.s3.eu-central-1.amazonaws.com/RaspberryPi-3-TorWiFi-20190721.7z)

Obviously, all buttons could be extended to dry contacts of driving relays, and LEDs - for driving relays, which making hat useful to monitor Raspberry status using simple discrete wires.

## RPMH services lifecycle
Most of RPMH services could be installed by script. But only one must be installed manually at end of `/etc/rc.local` - the one-liner which triggers up BOOT_OK LED. This is for triggering up BOOT_OK LED as last of, when system started up and initialized.
So, there boot-up sequence:
- Heartbeat service starting
- CPU temperature monitor starting
- IP Link monitor started
- TOR Link monitor started
- BOOT_OK triggered

At the shutdown/reboot triggered "Shutdown initiated" LED approx for 1 second and then all of LEDs are off.
"Overheat" LED is turned on at 75 more Celesius degrees, and turned off when temperature goes below 70 degrees.
Hearbeat LED flip-flopped each second (so, full cycle is 2 seconds)

## Related stuff
Board schematics obviously in `schematics` directory, and services - in `services`.
