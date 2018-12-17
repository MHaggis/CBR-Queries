# Carbon Black Response - Queries

Most recent queries may be found below.

* [Binary](binary.md)
* [Process](process.md)
* [emotet](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)

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


### Emotet

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\programdata\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:\appdata\roaming\


### dfsvc/browser broker queries

    parent_name:browser_broker.exe process_name:mshta.exe

<br>

    parent_name:browser_broker.exe process_name:rundll32.exe

<br>

    process_name:dfsvc.exe digsig_result_child:"Unsigned" OR digsig_result_child:"Untrusted Root"

<br>

    process_name:rundll32.exe childproc_name:dfsvc.exe
