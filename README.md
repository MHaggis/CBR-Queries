# Carbon Black Response - Queries

* [Binary](binary.md)
* [Process](process.md)
* [emotet](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)

Most recently added queries below.

### uacbypass

[Reference](https://enigma0x3.net/2016/08/15/fileless-uac-bypass-using-eventvwr-exe-and-registry-hijacking/)

    regmod:"mscfile\shell\open\command"

<br>

    parent_name:powershell.exe process_name:eventvwr.exe
