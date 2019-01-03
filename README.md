# Carbon Black Response - Queries

* [Binary](binary.md)
* [Process](process.md)
* [emotet](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)

Most recently added queries below.


### EternalBlue - Miner

[Reference](https://labsblog.f-secure.com/2019/01/03/nrsminer-updates-to-newer-version/)

    parent_name:wininit.exe process_name:spoolsv.exe

<br>

    process_name:sc.exe cmdline:Snmpstorsrv

<br>

    process_name:svchost.exe digsig_result_modload:unsigned


### SQLi Dumper + spam

    filemod:"url exploitables.xml"

<br>

    filemod:"url list.txt"

<br>

    process_name:"sqli dumper.exe"

<br>

    process_name:"advanced mass sender.exe"

<br>

    process_name:"turbomailer.exe"

<br>

    modload:"appvirtdll64_advanced mass sender.dll"

<br>

    process_name:storm.exe

### CobaltStrike - Argue

    (modload:"c:\windows\syswow64\ntmarta.dll") process_name:svchost.exe

<br>

    (modload:"c:\windows\system32\wshtcpip.dll") digsig_result:Unsigned (modload:"c:\windows\system32\wship6.dll")

<br>

    (modload:"c:\windows\syswow64\iertutil.dll" modload:"c:\windows\syswow64\ntmarta.dll") process_name:rundll32.exe

<br>

    (modload:"c:\windows\syswow64\iertutil.dll" modload:"c:\windows\syswow64\ntmarta.dll") process_name:rundll32.exe AND netconn_count:[1 TO * ]

<br>

    digsig_result_parent:Unsigned (process_name:svchost.exe -username:SYSTEM -username:"NETWORK SERVICE" -username:"LOCAL SERVICE" -cmdline:"UnistackSvcGroup")

<br>

    digsig_result_parent:Unsigned process_name:svchost.exe

<br>

    parent_name:rundll32.exe process_name:svchost.exe


### Process

    (regmod:"\registry\user\.default\software\microsoft\windows\currentversion\internet settings\proxyenable") digsig_result:Unsigned AND path:c:\windows\syswow64\*

<br>

    process_name:procdump.exe cmdline:-accepteula

<br>

    process_name:procdump.exe cmdline:lsass.exe

<br>

    digsig_result_parent:Unsigned process_name:explorer.exe

<br>

    process_name:schtasks.exe cmdline:/c

<br>

    process_name:schtasks.exe cmdline:"cscript.exe"

<br>

    process_name:schtasks.exe cmdline:"wscript.exe"

<br>

    process_name:schtasks.exe cmdline:"powershell.exe"


<br>

    crossproc_type:"remotethread" AND -process_name:wmiprvse.exe -process_name:svchost.exe -process_name:csrss.exe
