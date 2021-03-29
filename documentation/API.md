# API-Call Documentation
## Introduction
As many of us know YSFReflectors use the YSF protocol to communicate with endpoints. These original commands are well 
documented at http://ycs-wiki.xreflector.net/doku.php?id=start:protocols:ysf  thanks to the YCS-team for hosting them.
pYSFReflector has also an extended set of commands you can use for fetching information on the state of different things 
when running the reflector.

This document will show the commands, and the replies expected from the reflector.

## How To Issue A Call
First it is very easy to have a command sent to a reflector. Simply use a command similar to this:

`echo -n "YSFS" | nc -u 127.0.0.1 42000 -w 2 && echo`

or in a more general form:

`echo -n "<COMMAND>" | nc -u <IP-ADDRESS_OF_REFLECTOR> <PORT_OF_REFLECTOR> -w 2 && echo`

This line will send the chosen command to the reflector and prints out its reply.

## List Of Extended API-Commands
Here we will not describe the standard-commands in the YSF protocol, but the extended command set by the pYSFReflector.

The format of the answer will be the corresponding answer-code, and some values separated by `:` for each object in scope. 
Several objects are separated by `;`.

### QSRU - Query Reflector Uptime
#### Reply
`ASRU;57234;`

#### Description
Uptime of reflector in seconds

### QSRI - Query Reflector Info
#### Reply
`ASRI;62829:DE Germany:YSF262 BM263:pYSFReflector:20210326:1;`

#### Description
ID:Name:Description:Software-Name:Version:Status of Regular Expression Check (can be -1/0/1)

### QGWL - Query Gateway List
#### Reply
`AGWL;DL-LNK:161.97.73.43:57313;2622-DL:178.238.234.72:42000;DG9VH:84.58.124.6:42140;`

#### Description
Callsign:IP-Address:Port

### QLHL - Query Last Heard List
#### Reply
`ALHL;DG9VH:DG9VH:ALL:724:29-03-2021 07-32-13:0;2622-DL:DN3VH:ALL:723:29-03-2021 07-31-52:0;`

#### Description
Gateway:Callsign:Target:id_stream:StartTime:Duration

### QREJ - Query Rejected Callsigns/Gateways/IP-Addresses
#### Reply
`AREJ;DG9VH/CS:DG9VH400:ALL:-1:29-03-2021 12-17-08:-1;`

#### Description
Gateway/Rule that matched:Callsign:Target:Placeholder (Ignore):Timestamp:Placeholder (Ignore);

### QLHD - Query Last Heard List (with distinct callsigns)
#### Reply
`ALHD;2622-DL:DO7VN:ALL:2:29-03-2021 12-13-27:6;2622-DL:DH1VY:ALL:1:29-03-2021 11-45-30:0;`

#### Description
Gateway:Callsign:Target:id_stream:StartTime:Duration

### QRED - Query Rejected Callsigns/Gateways/IP-Addresses (with distinct data)
#### Reply
`ARED;DG9VH/CS:DG9VH1A:ALL:-1:29-03-2021 15-18-54:-1;`

#### Description
Gateway/Rule that matched:Callsign:Target:Placeholder (Ignore):Timestamp:Placeholder (Ignore);

### QACL - Query Access Control List-Statistics
#### Reply
`AACL;CS/2|AL/1|GW/1|IP/0;CS:DN3VH;CS:DG9VH;AL:N0CALL;GW:DN3VH;`

#### Description
CS/Number of muted Callsigns|AL/Number of whitelisted Callsigns|GW/Number of muted Gateways|IP/Number of muted IP-Addresses;List of Entries from deny.db
