### Mimikatz


    (modload:advapi32.dll AND modload:crypt32.dll AND modload:cryptdll.dll AND modload:gdi32.dll AND modload:imm32.dll AND modload:kernel32.dll AND modload:KernelBase.dll AND modload:msasn1.dll AND modload:msvcrt.dll AND modload:ntdll.dll AND modload:rpcrt4.dll AND modload:rsaenh.dll AND modload:samlib.dll AND modload:sechost.dll AND modload:secur32.dll AND modload:shell32.dll AND modload:shlwapi.dll AND modload:sspicli.dll AND modload:user32.dll AND modload:vaultcli.dll)

<br>

    digsig_result:"Unsigned" modload:samlib.dll modload:advapi32.dll

<br>

    (modload:advapi32.dll AND modload:crypt32.dll AND modload:cryptdll.dll AND modload:gdi32.dll AND modload:imm32.dll AND modload:kernel32.dll AND modload:KernelBase.dll AND modload:msasn1.dll AND modload:msvcrt.dll AND modload:ntdll.dll AND modload:rpcrt4.dll AND modload:rsaenh.dll AND modload:samlib.dll AND modload:sechost.dll AND modload:secur32.dll AND modload:shell32.dll AND modload:shlwapi.dll AND modload:sspicli.dll AND modload:user32.dll)

<br>

    process_name:lsass.exe filemod:c:\windows\system32\mimilsa.log
