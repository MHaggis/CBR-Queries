### Binary

    is_executable_image:"true"  digsig_result:"Unsigned"

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\windows\temp\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:\appdata\local\temp\

<br>

    is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\windows\syswow64

<br>

    (observed_filename:"c:\windows\system32\" OR observed_filename:"c:\windows\syswow64\") is_executable_image:"true" digsig_result:"Unsigned"



### Driver research

    /#/binaries/cb.urlver=1&q=observed_filename%3Ac%3A%5Cwindows%5Csystem32%5Cdrivers%5C&cb.q.digsig_result=(digsig_result%3A"Bad%20Signature"%20or%20digsig_result%3A"Invalid%20Signature"%20or%20digsig_result%3A"Invalid%20Chain"%20or%20digsig_result%3A"Untrusted%20Root"%20or%20digsig_result%3A"Explicit%20Distrust")&rows=10&start=0&sort=server_added_timestamp%20desc

<br>

    observed_filename:c:\windows\system32\drivers\

<br>

    observed_filename:c:\windows\system32\drivers\   digsig_result:"Explicit Distrust"

<br>

    (observed_filename:"c:\windows\system32\" OR observed_filename:"c:\windows\syswow64\") .sys

<br>

    (observed_filename:“c:\windows\syswow64\drivers”) .sys

<br>

    (observed_filename:"c:\windows\system32\drivers\") .sys digsig_sign_time:[* TO 2015-10-01T23:59:59]

<br>

    process_name:ntoskrnl.exe (digsig_result_modload:"Unsigned" OR digsig_result_modload:"Explicit\ Distrust")

<br>

    process_name:spoolsv.exe -digsig_result_modload:Signed

<br>

### Random

    company_name:“RW-Everything”
    internal_name:RwDrv.sys
    digsig_subject:“ChongKim Chan”
    digsig_sign_time:[* TO 2015-10-01T23:59:59]
