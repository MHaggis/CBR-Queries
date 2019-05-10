======================================
Invoke-AtomicRedTeam
======================================

Install Invoke-AtomicRedTeam
^^^^^^^^^

Get started with our simple Install script:

``powershell.exe "IEX (New-Object Net.WebClient).DownloadString('http://psInstall.AtomicRedTeam.com')"``

[Source](https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/execution-frameworks/Invoke-AtomicRedTeam/Install-AtomicRedTeam.ps1)

By default, it will download and Install Atomic Red Team to ``c:\AtomicRedTeam``

Running the [Install script](https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/execution-frameworks/Invoke-AtomicRedTeam/Install-AtomicRedTeam.ps1) locally provides three parameters:

InstallPath
- Where ART is to be Installed

    ``Install-AtomicRedTeam.ps1 -InstallPath c:\tools\``

DownloadPath
- Where ART is to be downloaded

    ``Install-AtomicRedTeam.ps1 -DownloadPath c:\tools\``

Verbose
- Verbose output during Installation

    ``Install-AtomicRedTeam.ps1 -verbose``

Manual Installation
___________________

    ``set-executionpolicy Unrestricted``

[PowerShell-Yaml](https://github.com/cloudbase/powershell-yaml) is required to parse Atomic yaml files:


    ``Install-Module -Name powershell-yaml``

    ``Import-Module .\Invoke-AtomicRedTeam.psm1``


Generate Tests
___________________

This process generates all Atomic tests and allows for easy copy and paste execution.
Note: you may need to change the path.

    ``Invoke-AllAtomicTests -GenerateOnly``

Execute All Tests
___________________

Execute all Atomic tests:

    ``Invoke-AllAtomicTests``

Execute All Tests - Specific Directory
___________________

Specify a path to atomics folder, example C:\AtomicRedTeam\atomics

    ``Invoke-AllAtomicTests -path C:\AtomicRedTeam\atomics``

Execute a Single Test
___________________

.. code-block:: console
    > powershell
    > $T1117 = Get-AtomicTechnique -Path ..\..\atomics\T1117\T1117.yaml
    > Invoke-AtomicTest $T1117


Additional Examples
___________________

If you would like output when running tests using the following:

#### Informational Stream

```powershell
Invoke-AtomicTest $T1117 -InformationAction Continue
```

#### Verbose Stream

```powershell
Invoke-AtomicTest $T1117 -Verbose
```

#### Debug Stream

```powershell
Invoke-AtomicTest $T1117 -Debug
```

#### WhatIf

If you would like to see what would happen without running the test

```powershell
Invoke-AtomicTest $T1117 -WhatIf
```

#### Confirm

To run all tests without confirming them run using the Confirm switch to false

```powershell
Invoke-AtomicTest $T1117 -Confirm:$false
```

Or you can set your `$ConfirmPreference` to 'Medium'

```powershell
$ConfirmPreference = 'Medium'
Invoke-AtomicTest $T1117
```






The EQL library current supports Python 2.7 and 3.5 - 3.7. Assuming a supported Python version is installed, run the command:

.. code-block:: console

    $ git clone https://github.com/endgameinc/eqllib
    $ cd eqllib
    $ python setup.py install

If Python is configured and already in the PATH, then ``eqllib`` will be readily available, and can be checked by running the command:

.. code-block:: console

    $ eqllib -h
    usage: eqllib [-h] {convert-query,convert-data,query,survey} ...

    EQL Analytics

    positional arguments:
      {convert-query,convert-data,query,survey}
                            Sub Command Help
        convert-query       Convert a query to specific data source
        convert-data        Convert data from a specific data source
        query               Query over a data source
        survey              Run multiple analytics over JSON data

.. toctree::
   :maxdepth: 2
   :caption: Contents

   cli
   sysmon
