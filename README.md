# Carbon Black Response - Queries

Most recent queries may be found below.

* [Binary](binary.md)
* [Process](process.md)
* [emotet](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)

### Process

    crossproc_type:"remotethread" AND -process_name:wmiprvse.exe -process_name:svchost.exe -process_name:csrss.exe


### Coin Miner

    digsig_result:"Unsigned" company_name:"Zhuhai Kingsoft Office Software Co.,Ltd"

<br>

    parent_name:lsass.exe process_name:cmd.exe childproc_name:reg.exe

<br>

    parent_name:lsass.exe process_name:cmd.exe childproc_name:schtasks.exe

<br>

    process_name:net1.exe cmdline:"net1 user IISUSER_ACCOUNTXX /del"

<br>

    process_name:lsass.exe digsig_result_filewrite:"Unsigned"

<br>

    company_name:"TODO: <公司名>"

<br>

    parent_name:conhost.exe digsig_result_parent:"Unsigned"


https://github.com/fireice-uk/xmr-stak

<br>

    filemod:xmrstak_opencl_backend.dll

<br>

    filemod:xmrstak_cuda_backend.dll

<br>

    observed_filename:c:\windows\debug\

<br>

    observed_filename:c:\windows\inf\

<br>

    observed_filename:c:\windows\web\


### Emotet / qakbot

    digsig_publisher:"Evaila IT Ltd"

<br>

    process_name:wmiprvse.exe modload:c:\windows\temp\* digsig_result_modload:Unsigned

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\programdata\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:\appdata\roaming\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:C:\Windows\SysWOW64\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:C:\Windows\system32\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:C:\Windows\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:C:\Windows\temp
