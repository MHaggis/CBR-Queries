# Carbon Black Response - Queries

Most recent queries may be found below.

* [Binary](binary.md)
* [Process](process.md)
* [emotet](emotet.md)
* [mimikatz](mimikatz.md)
* [helpers](helpers.md)


### dfsvc/browser broker queries

    parent_name:browser_broker.exe process_name:mshta.exe

<br>

    parent_name:browser_broker.exe process_name:rundll32.exe

<br>

    process_name:dfsvc.exe digsig_result_child:"Unsigned" OR digsig_result_child:"Untrusted Root"

<br>

    process_name:rundll32.exe childproc_name:dfsvc.exe
