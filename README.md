radiator-fticks-anonymizer
==========================

Radiator hook to anonymize MAC address before sending to F-Ticks.

This hook anonymizes the MAC address so the user data can be sent upstream  without violating the users privacy.

To use this hook you need to specify a key in the radiator config:
DefineGlobalVar FTicks_hash_key KEY

The default behaviour is to save the vendor part of the address and hash the rest.
If you like to hash the whole address you can add do this by adding following to the radiator config:
DefineGlobalVar FTicks_hash_all yes

Then use it as a ordinary hook:
PostAuthHook file:"/local/radiator/hooks/fticks_anonymizer"

And syslog with the new hashed variable created in the hook (X-Calling-Station-Id-Hashed):
SuccessFormat F-TICKS/eduroam/1.0#REALM=%R#VISCOUNTRY=%{eduroam-SP-Country}#VISINST=%{Operator-Name}#CSI=%{X-Calling-Station-Id-Hashed}#RESULT=OK#
FailureFormat F-TICKS/eduroam/1.0#REALM=%R#VISCOUNTRY=%{eduroam-SP-Country}#VISINST=%{Operator-Name}#CSI=%{X-Calling-Station-Id-Hashed}#RESULT=FAIL#

F-Ticks
-------
Read more about F-Ticks
http://monitor.eduroam.org/f-ticks/

Configure F-Ticks in Radiator
https://confluence.terena.org/display/H2eduroam/radiator-flr

