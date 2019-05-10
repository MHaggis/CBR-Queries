# Carbon Black Response - Queries

* [Binary](binary.md)
* [Process](process.md)
* [malware](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)
* [Certificates](Certs.md)

Most recently added queries below.

`is_executable_image_filewrite:true AND process_name:powershell.exe`

`cmdline:--* AND netconn_count:[2 TO *] AND modload:"c:\windows\syswow64\bcrypt.dll" AND digsig_result:"Untrusted Root"`

###

`process_name:winword.exe regmod:software\microsoft\windows\currentversion\run\* modload:vbe*.dll`

`parent_name:winword.exe regmod:software\microsoft\windows\currentversion\run\* childproc_name:winword.exe childproc_name:cmd.exe`

`process_name:regsvr32.exe AND cmdline:f1 AND childproc_name:rundll32.exe AND childproc_count:[2 TO *]`
