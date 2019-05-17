# Carbon Black Response - Queries

* [Binary](binary.md)
* [Process](process.md)
* [malware](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)
* [Certificates](Certs.md)

Most recently added queries below.

Eternalblue-Doublepulsar-Metasploit

[reference](https://github.com/ElevenPaths/Eternalblue-Doublepulsar-Metasploit/tree/master/deps)
[reference](https://gist.github.com/misterch0c/08829bc65b208609d455a9f4aeaa2a6c)
filemod:
```
etebcore-2.x86.dll  
eternalblue-2.2.0.fb  
eternalchampion-2.0.0.fb
```

modload:
```
trch-1.dll
libxml2.dll
tucl-1.dll
coli-0.dll
exma-1.dll
tibe-2.dll
cnli-1.dll
xdvl-0.dll
crli-0.dll
ssleay32.dll
libeay32.dll
trfo-2.dll
posh-0.dll
ucl.dll
zlib1.dll
```
_______

`(regmod:"\registry\machine\software\microsoft\windows defender security center\notifications\disablenotifications")`

`(regmod:"\registry\machine\software\policies\microsoft\windows defender\disableantispyware")`

`is_executable_image_filewrite:true AND process_name:powershell.exe`

`cmdline:--* AND netconn_count:[2 TO *] AND modload:"c:\windows\syswow64\bcrypt.dll" AND digsig_result:"Untrusted Root"`

###

`process_name:winword.exe regmod:software\microsoft\windows\currentversion\run\* modload:vbe*.dll`

`parent_name:winword.exe regmod:software\microsoft\windows\currentversion\run\* childproc_name:winword.exe childproc_name:cmd.exe`

`process_name:regsvr32.exe AND cmdline:f1 AND childproc_name:rundll32.exe AND childproc_count:[2 TO *]`
