# Carbon Black Response - Queries

* [Binary](binary.md)
* [Process](process.md)
* [malware](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)
* [Certificates](certs.md)

Most recently added queries below.

## New stuff

`process_name:msbuild.exe digsig_result_modload:Unsigned parent_name:cmd.exe`

`process_name:msbuild.exe crossproc_name:notepad.exe`

`process_name:msbuild.exe (parent_name:powershell.exe OR parent_name:cmd.exe)`

`process_name:msbuild.exe AND crossproc_type:"remotethread"`



## Things

 `process_name:rundll32.exe modload:amsi.dll`

`process_name:rundll32.exe (modload:scrobj.dll OR modload:clr.dll)`

`process_name:rundll32.exe (modload:scrobj.dll OR modload:clr.dll) -username:SYSTEM cmdline:advpack.dll`

`process_name:rundll32.exe (modload:scrobj.dll OR modload:clr.dll)  cmdline:ieadvpack.dll`

`process_name:rundll32.exe (modload:scrobj.dll OR modload:clr.dll)  cmdline:syssetup.dll`

`process_name:cscript.exe (modload:scrobj.dll AND modload:clr.dll)`

`parent_name:cmd.exe process_name:installutil.exe modload:clr.dll -username:SYSTEM`

`process_name:installutil.exe modload:clr.dll -username:SYSTEM -cmdline:realtek`

`parent_name:cmd.exe process_name:installutil.exe modload:clr.dll`

`process_name:installutil.exe modload:clr.dll -username:SYSTEM cmdline:.dll`

`process_name:installutil.exe cmdline:.dll -username:SYSTEM`


## stuff

`process_name:excel.exe|winword.exe|powerpnt.exe (cmdline:.dll OR cmdline:.exe)`

`process_name:control.exe`

`process_name:winword.exe cmdline:http:\`

`parent_name:winword.exe process_name:rundll32.exe netconn_count:[1 TO *]`

`"C:\Windows\system32\rundll32.exe" Shell32.dll,Control_RunDLL c:\users\public\test2.dll`


`modload:mscor* AND modload:clr.dll AND -process_name:mscorsvw.exe AND path:c:\users* AND modload:samlib.dll`


## wscript stuff

`internal_name:wscript.exe -process_name:wscript.exe`

`parent_name:taskeng.exe internal_name:wscript.exe -process_name:wscript.exe`

`path:AppData\Roaming\*`

`internal_name:schtasks.exe -process_name:schtasks.exe`

## Check Yo RDP

`-file_version:6.1.7601.24441 observed_filename:termdd.sys`

## Conhost

`childproc_name:conhost.exe`


## Eternalblue-Doublepulsar-Metasploit

- [reference](https://github.com/ElevenPaths/Eternalblue-Doublepulsar-Metasploit/tree/master/deps)
- [reference](https://gist.github.com/misterch0c/08829bc65b208609d455a9f4aeaa2a6c)

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
