======================================
Invoke-AtomicRedTeam
======================================

Install Invoke-AtomicRedTeam
^^^^^^^^^

Get started with our simple Install script:

``powershell.exe "IEX (New-Object Net.WebClient).DownloadString('http://psInstall.AtomicRedTeam.com')"``

`Source <https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/execution-frameworks/Invoke-AtomicRedTeam/Install-AtomicRedTeam.ps1>`_

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

Informational Stream
___________________

.. code-block:: console

    > powershell
    > Invoke-AtomicTest $T1117 -InformationAction Continue

Verbose Stream
___________________

.. code-block:: console

    > powershell
    > Invoke-AtomicTest $T1117 -Verbose

Debug Stream
___________________

.. code-block:: console

    > powershell
    > Invoke-AtomicTest $T1117 -Debug

WhatIf
___________________

If you would like to see what would happen without running the test

.. code-block:: console

    > powershell
    > Invoke-AtomicTest $T1117 -WhatIf

Confirm
___________________

To run all tests without confirming them run using the Confirm switch to false

.. code-block:: console

    > powershell
    > Invoke-AtomicTest $T1117 -Confirm:$false

Or you can set your `$ConfirmPreference` to 'Medium'

.. code-block:: console

    > powershell
    > $ConfirmPreference = 'Medium'
    > Invoke-AtomicTest $T1117

.. toctree::
   :maxdepth: 2
   :caption: Contents

   cli
   sysmon
