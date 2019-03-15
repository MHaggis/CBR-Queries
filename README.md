# Carbon Black Response - Queries

* [Binary](binary.md)
* [Process](process.md)
* [malware](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)

Most recently added queries below.

###

`process_name:explorer.exe filemod:temp1_*.zip filemod:request*.doc`

`process_name:winword.exe cmdline:request*.doc\"`

`process_name:explorer.exe filemod:temp1_*.zip filemod:request*.doc`

###

`process_name:mode.com`

`digsig_result_parent:Unsigned process_name:raserver.exe`



### scrobj load and behavior

`process_name:regsvr32.exe (modload:scrobj.dll) AND childproc_name:powershell.exe`

`parent_name:powershell.exe AND process_name:nslookup.exe AND netconn_count:[1 TO *]`

### Java Embedded MSI files
`process_name:java.exe cmdline:-classpath parent_name:javaw.exe (childproc_name:java.exe or childproc_name:conhost.exe)`

`process_name:java.exe cmdline:-classpath parent_name:javaw.exe (childproc_name:java.exe or childproc_name:conhost.exe) filemod:appdata\local\temp\*.class`

[API](https://github.com/cparmn/CarbonBlackResponse/blob/master/msijar.py)




### Qakbot/Emotet/malware?

`process_name:explorer.exe filemod:.wpq`
`process_name:explorer.exe filemod:.wpl`
`process_name:explorer.exe filemod:.dll`
`process_name:explorer.exe filemod:.dat`

`process_name:explorer.exe filemod:bot_serv[1]`
`process_name:explorer.exe filemod:t3[1]`


`process_name:schtasks.exe (cmdline:powershell.exe OR cmdline:$windowsupdate OR cmdline:.wpq OR cmdline:.wpl)`

Binary:

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


process:

`cmdline:$windowsupdate*`

`process_name:schtasks.exe cmdline:WEEKLY`


### uacbypass

[Reference](https://enigma0x3.net/2016/08/15/fileless-uac-bypass-using-eventvwr-exe-and-registry-hijacking/)

    regmod:"mscfile\shell\open\command"

<br>

    parent_name:powershell.exe process_name:eventvwr.exe
