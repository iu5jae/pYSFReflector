# pYSFReflector
This is a YSF Reflector implemented in python3, mainly compatible with g4klx reflector.

## Additional Features
### Enhanced Blocking List
With the enhanced blocking list you are able to mute calls based on

* callsign of sender
* callsign of gateway used
* ip-address of gateway

### Blocking On Regular Expression Callsign Check
It is also possible to use (by default enabled in the YSFReflector.ini) a callsign check based on a regular expression to check the callsign plausibility in callsign-format and length.

The result of this check can be overdriven by a whitelist-entry in the blocklist (for example: N0CALL is blocked by default by this expression but could be allowed for special bridging situations).

### Muting Matrix
Here you see a matrix documenting the behavior of the blocking-lists and configuration of regular expression (RE)-check:

![Muting-Matrix](img/Muting-Matrix.png "Muting-Matrix")

Within this table following descriptions for the cell-values should help understanding the table:
* X: Any value
* YES: set and matches with callsign/gateway/ip-address	
* NO: not set	
* 1: check via RE enabled, normal operation	
* 0: check via RE disabled, but passes everything	
* -1: check via RE disabled, but only pass whitelist	

### Avoiding Parallel Incomming Transmissions
There is also a functionality implemented that prohibits parallel transmissions that can happen if two senders transmit at the same time. Here the principle 'first-comes-first-serves' is realized, so the second station in time will just be muted to not disturb the audio.

## Easy Installation And Upgrade
Depending on your used operating system and python3-installation you just have to take care that following libraries are installed:

* socket
* threading
* queue
* sys
* os
* time
* re
* configparser
* datetime
* signal
* datetime
* bisect
* struct

In most installations this packages are already installed, otherwise you easily can install them with your system-package-manager (for example Debian: apt) or you use pip3 install <package>-command.

The configuration file (YSFReflector.ini) is based on the origin YSFReflector.ini of G4KLX's YSFReflector but with added new configuration-items. So If you know the old reflector-software - configuring this one would be straight forward.
