# Carbon Black Response - Queries

* [Binary](binary.md)
* [Process](process.md)
* [malware](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)

Most recently added queries below.

### Qakbot/Emotet/malware?

Binary:

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
