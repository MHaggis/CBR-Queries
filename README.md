# Carbon Black Response - Queries

Analyzing Carbon Black Response endpoint telemetry in Splunk


### dfsvc/browser broker queries

    parent_name:browser_broker.exe process_name:mshta.exe

<br>

    parent_name:browser_broker.exe process_name:rundll32.exe

<br>

    process_name:dfsvc.exe digsig_result_child:"Unsigned" OR digsig_result_child:"Untrusted Root"

<br>

    process_name:rundll32.exe childproc_name:dfsvc.exe


### Process

    process_name:lsass.exe digsig_result_filewrite:"Unsigned"

<br>

    process_name:lsass.exe AND digsig_result_modload:"Unsigned"

<br>

    filemod:Content.Outlook\*  and is_executable_image_filewrite:True

<br>

    filemod:Content.Outlook\*  and -digsig_result_filewrite:Signed

<br>

    process_name:winlogon.exe AND netconn_count:[1 TO *]

<br>

    is_executable_image_filewrite:True -path:google\chrome\* and -path:google\update\* -digsig_result_filewrite:Signed filemod:local\settings\* filemod:appdata\local\temp\*

<br>

    filemod: “Start Menu\Programs\Startup”

<br>

    regmod:CurrentVersion\Run*

<br>

    filemod:windows\system32\* digsig_result:unsigned digsig_result_filewrite:"Unsigned"

<br>

    regmod:services\national* digsig_result:unsigned

<br>

    regmod:services\svchostc* digsig_result:unsigned

<br>

    path:windows\system32\* digsig_result:unsigned parent_name:services.exe childproc_count:1

## Emotet

    -parent_name:perccli64.exe -parent_name:kix32.exe -parent_name:activrelay.exe digsig_result_parent:"Unsigned"

<br>

    digsig_result_parent:"Unsigned" digsig_result_process:"Unsigned" digsig_result_child:"Unsigned"

<br>

    digsig_result:"Unsigned" filemod:c:\windows\syswow64\*

<br>

    (modload:"c:\windows\system32\wow64cpu.dll") digsig_result_process:"Unsigned" digsig_result_parent:"Unsigned"

<br>

    digsig_result:"Unsigned" filemod:c:\programdata\*

<br>

    digsig_result_process:Unsigned parent_name:services.exe

<br>

    parent_name:taskeng.exe digsig_result_process:Unsigned -process_name:currentdefsloader.exe -process_name:sqltasks.exe

<br>

    (company_name:"Fatal Enterprice" OR company_name:"FastSpring Past" OR company_name:"Qualifacts Systems Plane" OR company_name:"WehwGWE.hWRGW" OR company_name:"Microsoft Co" OR company_name:"WMI" OR company_name:"SimVentions Hole" OR company_name:"Microsoft Corporatio" OR company_name:"Win Interactive LLC* Right" OR company_name:"PERCo-SC-610T/L" OR company_name:"Hekuriporuc Ltd." OR company_name:"Hikaham Ltd." OR company_name:"С Corporation" OR company_name:"Roni Enterprice" OR company_name:"Conoha.jp" OR company_name:"P.A.C. Nichols" OR company_name:"Server Service Core DLL" OR company_name:"NTLM Shared Functionality" OR company_name:"ImTOO Software Studio" OR company_name:"TeamViewer GmbH" OR company_name:"BST" OR company_name:"America Online, Inc.")

## Regular Proc search

    (regmod:"\registry\user\s-1-5-21-348440682-330175067-1304115618-242891\software\microsoft\office\14.0\excel\security\accessvbom")

<br>

    (process_name:cmd.exe OR process_name:powershell.exe OR process_name:wmic.exe OR process_name:msbuild.exe OR process_name:mshta.exe OR process_name:wscript.exe OR process_name:cscript.exe OR process_name:installutil.exe OR process_name:rundll32.exe OR process_name:regsvr32.exe OR process_name:msxsl.exe OR process_name:regasm.exe OR process_name:regsvcs.exe) (domain:pastebin.com OR domain:dl.dropboxusercontent.com OR domain:githubusercontent.com)

<br>

    digsig_result_child:"Unsigned" ((parent_name:chrome.exe OR parent_name:firefox.exe OR parent_name:iexplore.exe OR parent_name:microsoftedge.exe OR parent_name:outlook.exe) is_executable_image_filewrite:"true")

<br>

    digsig_result_process:"Unsigned" ((parent_name:chrome.exe OR parent_name:firefox.exe OR parent_name:iexplore.exe OR parent_name:microsoftedge.exe OR parent_name:outlook.exe) is_executable_image_filewrite:"true")

<br>

    regmod:"keyboard layout\2"

<br>

    (regmod:"\registry\machine\software\microsoft\windows nt\currentversion\image file execution options\cmd.exe\verifierdlls")

<br>

    process_name:mshta.exe modload:mscoree.dll

<br>

    (modload:mscoree.dll AND modload:system.management.automation.dll) -process_name:powershell_ise.exe -process_name:sdiagnhost.exe -process_name:mscorsvw.exe -process_name:powershell.exe -process_name:searchfilterhost.exe

<br>

    process_name:netsh.exe cmdline:appdata/

<br>

    (modload:mscoree.dll AND modload:system.management.automation.dll AND modload:mscorlib*) -process_name:powershell_ise.exe -process_name:sdiagnhost.exe -process_name:mscorsvw.exe -process_name:powershell.exe -process_name:searchfilterhost.exe

<br>

    (cmdline:/user: OR cmdline:/pwd: OR cmdline:/username: OR cmdline:/password:)

<br>

    process_name:notepad.exe (modload:vaultcli.dll AND modload:samlib.dll)

<br>

    parent_name:explorer.exe process_name:lsass.exe

<br>

    process_name:netsh.exe cmdline:ProgramData/

<br>

    process_name:csc.exe netconn_count:[1 TO *]

<br>

    path:programdata\* -path:programdata\*\* -process_name:chgservice.exe -process_name:userprofilemigrationservice.exe -process_name:mm.exe -process_name:mmimage.exe

<br>

    process_name:rundll32.exe domain:.ru AND netconn_count:[1 TO *]

<br>

    (process_name:powershell.exe OR internal_name:powershell) (modload:samlib.dll OR modload:vaultcli.dll)

<br>

    parent_name:spoolsv.exe (process_name:cmd.exe OR process_name:powershell.exe)

<br>

    digsig_result:Unsigned ipport:443 modload:winsta.dll path:appdata/local/temp/*

### BloodHound detection - network

    ipport:445 AND netconn_count:[150 TO *] AND -process_name:ntoskrnl.exe AND process_name:*

### BloodHound detection - command line

    cmdline:--ExcludeDC OR cmdline:LoggedOn OR cmdline:ObjectProps OR cmdline:GPOLocalGroup OR product_name:"SharpHound"

### BloodHound detection - file modifications

    filemod:sessions.csv OR filemod:acls.csv OR filemod:group_membership.csv OR filemod:local_admins.csv OR filemod:computer_props.csv OR filemod:user_props.csv

### BloodHound detection - network pipe

    filemod:\pipe\samr AND filemod:\pipe\lsarpc AND filemod:pipe\srvsvc

<br>

    netconn_count:[100 TO *] AND ipport:445 AND (filemod:lsarpc OR filemod:samr OR filemod:srvsvc)

### Squiblytwo

    (process_name:wmic.exe OR internal_name:wmic.exe) (cmdline:format:\ AND cmdline:os)

<br>

    (process_name:wmic.exe OR internal_name:wmic.exe) (cmdline:format:\ AND cmdline:os) AND netconn_count:[1 TO *]

<br>

    (process_name:wmic.exe OR internal_name:wmic.exe) netconn_count:[1 TO *]

<br>

    process_name:wmic.exe (modload:jscript.dll OR modload:vbscript.dll)

<br>

    process_name:powershell.exe (filemod:c:\windows\temp\*)

<br>

    process_name:powershell.exe ipport:445

<br>

    process_name:powershell.exe AND netconn_count:[2 TO *] ipport:445

<br>

    process_name:powershell.exe AND netconn_count:[2 TO *] (ipport:445 OR ipport:80 OR ipport:443 OR ipport:137 OR ipport:138 OR ipport:135 OR ipport:22)

<br>

    (process_name:powershell.exe or process_name:powershell_ise.exe) AND netconn_count:[2 TO *] (ipport:445 OR ipport:80 OR ipport:443 OR ipport:137 OR ipport:138 OR ipport:135 OR ipport:22)

<br>

    parent_name:explorer.exe process_name:mshta.exe (modload:jscript.dll OR modload:vbscript.dll) netconn_count:[1 TO *]

<br>

    process_name:mshta.exe (modload:jscript.dll OR modload:vbscript.dll) netconn_count:[1 TO *]

<br>

    process_name:php.exe childproc_name:cmd.exe

<br>

    parent_name:php.exe process_name:cmd.exe

<br>

    parent_name:php.exe process_name:cmd.exe digsig_result_child:"Unsigned"

<br>

    (filemod:wwwroot\* or filemod:htdocs\*) and (filemod:.aspx or filemod:.jsp or filemod:.cfm or filemod:.asp or filemod:.php) AND host_type:"server"

<br>

    parent_name:outlook.exe (process_name:iexplore.exe OR process_name:chrome.exe OR process_name:microsoftedge.exe OR process_name:firefox.exe)

### Mimikatz


    (modload:advapi32.dll AND modload:crypt32.dll AND modload:cryptdll.dll AND modload:gdi32.dll AND modload:imm32.dll AND modload:kernel32.dll AND modload:KernelBase.dll AND modload:msasn1.dll AND modload:msvcrt.dll AND modload:ntdll.dll AND modload:rpcrt4.dll AND modload:rsaenh.dll AND modload:samlib.dll AND modload:sechost.dll AND modload:secur32.dll AND modload:shell32.dll AND modload:shlwapi.dll AND modload:sspicli.dll AND modload:user32.dll AND modload:vaultcli.dll)

<br>

    digsig_result:"Unsigned" modload:samlib.dll modload:advapi32.dll

<br>

    (modload:advapi32.dll AND modload:crypt32.dll AND modload:cryptdll.dll AND modload:gdi32.dll AND modload:imm32.dll AND modload:kernel32.dll AND modload:KernelBase.dll AND modload:msasn1.dll AND modload:msvcrt.dll AND modload:ntdll.dll AND modload:rpcrt4.dll AND modload:rsaenh.dll AND modload:samlib.dll AND modload:sechost.dll AND modload:secur32.dll AND modload:shell32.dll AND modload:shlwapi.dll AND modload:sspicli.dll AND modload:user32.dll)

<br>

    process_name:lsass.exe filemod:c:\windows\system32\mimilsa.log

### Helpers

    netconn_count:[1 TO *] (ipport:80 OR ipport:443)

<br>

    ipaddr:10.0.0.0/8 ipaddr:192.168.0.0/16 ipaddr:172.16.0.0/12

### Network

<br>

    domain:.ru -process_name:iexplore.exe OR -process_name:chrome.exe OR -process_name:microsoftedge.exe OR -process_name:microsoftedgecp.exe OR -process_name:firefox.exe OR -process_name:opera.exe digsig_result:Unsigned

### Binary

    is_executable_image:"true"  digsig_result:"Unsigned"

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\windows\temp\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:\appdata\local\temp\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\windows\syswow64


### Driver research

    /#/binaries/cb.urlver=1&q=observed_filename%3Ac%3A%5Cwindows%5Csystem32%5Cdrivers%5C&cb.q.digsig_result=(digsig_result%3A"Bad%20Signature"%20or%20digsig_result%3A"Invalid%20Signature"%20or%20digsig_result%3A"Invalid%20Chain"%20or%20digsig_result%3A"Untrusted%20Root"%20or%20digsig_result%3A"Explicit%20Distrust")&rows=10&start=0&sort=server_added_timestamp%20desc

<br>

    observed_filename:c:\windows\system32\drivers\

<br>

    observed_filename:c:\windows\system32\drivers\   digsig_result:"Explicit Distrust"

<br>

    (observed_filename:"c:\windows\system32\" OR observed_filename:"c:\windows\syswow64\") .sys

<br>

    (observed_filename:“c:\windows\syswow64\drivers”) .sys

<br>

    (observed_filename:"c:\windows\system32\drivers\") .sys digsig_sign_time:[* TO 2015-10-01T23:59:59]

<br>

    process_name:ntoskrnl.exe (digsig_result_modload:“Unsigned” OR digsig_result_modload:"Explicit Distrust")


### Rogue DC

    process_name:svchost.exe AND cmdline:"-k netsvcs -p -s gpsvc" AND domain:* AND -(ipaddr:172.20.1.200 OR ipaddr:10.100.12.4 OR ipaddr:172.20.0.117 OR ipaddr:10.100.86.75 OR ipaddr:10.254.1.120 OR ipaddr:10.254.1.69 OR ipaddr:10.254.1.121)

<br>

    process_name:svchost.exe AND cmdline:"-k netsvcs -p -s gpsvc" AND domain:* AND -host_type:"domain_controller"

### Rando

    company_name:“RW-Everything”
    internal_name:RwDrv.sys
    digsig_subject:“ChongKim Chan”
    digsig_sign_time:[* TO 2015-10-01T23:59:59]
