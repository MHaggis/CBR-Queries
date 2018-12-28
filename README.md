# Carbon Black Response - Queries

Most recent queries may be found below.

* [Binary](binary.md)
* [Process](process.md)
* [emotet](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)


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

    
