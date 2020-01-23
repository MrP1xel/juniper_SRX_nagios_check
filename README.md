This is as Nagios script written in Python for Juniper SRX serie monitoring using SNMP

usage: snmp_juniper_new.py [-h] [-cpu CPU] [-host HOST] [-community COMMUNITY]
                           [-warning WARNING] [-critical CRITICAL]

optional arguments:
  -h, --help            show this help message and exit
  -cpu CPU              CPU average
  -host HOST            host IP
  -community COMMUNITY  SNMP community of the device
  -warning WARNING      warning level
  -critical CRITICAL    critical level

For the moment, the script report only CPU average usage for 1 minute,5 minutes and 15 minutes (with perfdata)

You need to specify :

* the host IP with the option -host
* the SNMP community with -community
* warning level with -warning
* critical level with -critical
* the option -cpu 1 (this is for now the only data received)

