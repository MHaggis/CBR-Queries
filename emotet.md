## Malware

Not 100% these are emotet. It's highly possible Ryuk, Qakbot and Trickbot are mixed in here.

### Trickbot

`(ipport:447 OR ipport:449) process_name:svchost.exe filemod:injectdll64_configs*`

`filemod: c:\windows\temp\*.bat`

Catches all the BAT's being written to \temp

### OrangeWorm

`process_name:rundll32.exe cmdline:ControlTrace AND childproc_count:[2 TO *] AND regmod_count:[1 TO *]`

`company_name:"Indiana Software Foundation"`

`(observed_filename:"c:\windows\system32\" OR observed_filename:"c:\windows\syswow64\") is_executable_image:"true" digsig_result:"Unsigned"`

### Qakbot/Emotet/malware?

`process_name:explorer.exe filemod:.wpq`
`process_name:explorer.exe filemod:.wpl`
`process_name:explorer.exe filemod:.dll`
`process_name:explorer.exe filemod:.dat`

`process_name:explorer.exe filemod:bot_serv[1]`
`process_name:explorer.exe filemod:t3[1]`


`process_name:schtasks.exe (cmdline:powershell.exe OR cmdline:$windowsupdate OR cmdline:.wpq OR cmdline:.wpl)`


`company_name:"Borland Corporation"`

`digsig_publisher:"RMBMS Limited"`

`digsig_publisher:"PROVERA LIMITED"`

`is_executable_image:"true" digsig_result:Unsigned observed_filename:\AppData\Roaming\Microsoft\`

`digsig_publisher:"Skotari Limited"`

`digsig_issuer:"Sectigo RSA Code Signing CA"`

`digsig_issuer:"COMODO RSA Code Signing CA"`

`digsig_subject:"Skotari Limited"`

`digsig_publisher:"IMRAN IT SERVICES LTD"`



```is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c$```

```is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:admin$```

```is_executable_image:"true"  digsig_result:"Unsigned"```

```is_executable_image:"true"  digsig_result:"Signed"```

`cmdline:$windowsupdate*`

`process_name:schtasks.exe cmdline:WEEKLY`


    digsig_publisher:"Evaila IT Ltd"

<br>

    digsig_issuer:"COMODO RSA Code Signing CA"


<br>

    process_name:wmiprvse.exe modload:c:\windows\temp\* digsig_result_modload:Unsigned

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\programdata\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:\appdata\roaming\

<br>

    is_executable_image:"true" digsig_result:Unsigned observed_filename:\AppData\Roaming\Microsoft\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:C:\Windows\SysWOW64\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:C:\Windows\system32\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:C:\Windows\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:C:\Windows\temp

<br>

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
