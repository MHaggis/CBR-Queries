======================================
Getting Started with Carbon Black Response and Hunting
======================================

Data analysis is a cyclical process. I recommend following a similar process:

.. image:: https://redcanary.com/wp-content/uploads/ProcessFlow.png

`reference blog post <https://redcanary.com/blog/carbon-black-response-with-splunk-advanced-data-analysis/>`_

1. Decide what to look for (hypothesis, situational awareness)
2. Tune, focus query, Alert
3. Investigate
4. Tune alert
5. Measure Progress

Decide what to look for (hypothesis, situational awareness)
^^^^^^^^^

With Carbon Black Response I start all my hunts with the binary store. Most analysts ignore it, but I find it to be one of the most important data collected.

Begin by viewing `Binary Queries <https://github.com/MHaggis/CBR-Queries/blob/master/binary.md>`. My most frequented query to start with is -

.. code-block:: console

    > is_executable_image:"true"  digsig_result:"Unsigned"

Microsoft caveats -

* catalog signed
* Authenticode

tl;dr - understand legitimate Microsoft binaries may be seen/found as "Unsigned".

Back to our query above. Begin previewing all binaries. In CBR, by default our view shows us "company_name" under disig_status on the right. I compare the binary name + company_name. If company_name is not present on the right, does the binary name look legitimate? Is it camel case? Does it look suspicious?
If the file raises suspicion, I will open it in a new tab and continue to review binary pages.
If there is too many binaries to review, I will begin to narrow my search by using queries such as -

.. code-block:: console

    > is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\windows\temp\
    > is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:\appdata\local\temp\
    > is_executable_image:"true"  digsig_result:"Unsigned" observed_filename:c:\windows\syswow64
    > (observed_filename:"c:\windows\system32\" OR observed_filename:"c:\windows\syswow64\") is_executable_image:"true" digsig_result:"Unsigned"

Notice the usage of ``observed_filename`` - this is similar to defining ``path`` in process search. Fortunately, in binary search we do not have to give it a filename, but just the path (``appdata\local\``).

Identify Suspicious Drivers
^^^^^^^^^

Hunting for Suspicious Drivers is extremely rewarding, but I would be lying if it wasn't one of the hardest types of hunts to perform.

All queries may be found `here <https://github.com/MHaggis/CBR-Queries/blob/master/binary.md>`_

Binary
_______

To begin, I recommend starting with ``digsig_result`` on files in ``observed_filename:c:\windows\system32\drivers\`` -

.. code-block:: console

    >   observed_filename:c:\windows\system32\drivers\   digsig_result:"Bad Signature"  digsig_result:"Invalid Signature"  digsig_result:"Invalid Chain"  digsig_result:"Untrusted Root"  digsig_result:"Explicit Distrust"

Instead of copy/paste the query, I paste this in the URL bar:

``/#/binaries/cb.urlver=1&q=observed_filename%3Ac%3A%5Cwindows%5Csystem32%5Cdrivers%5C&cb.q.digsig_result=(digsig_result%3A"Bad%20Signature"%20or%20digsig_result%3A"Invalid%20Signature"%20or%20digsig_result%3A"Invalid%20Chain"%20or%20digsig_result%3A"Untrusted%20Root"%20or%20digsig_result%3A"Explicit%20Distrust")&rows=10&start=0&sort=server_added_timestamp%20desc``

I left out ``digsig_result:"Expired"`` as it gets noisy. Once reviewing the other 5, I add Expired and review the data.

This process can take time as drivers either look normal or evil. Upon identifying a suspicious driver, open it up in a new tab, review it, look it up on VT (Google, etc) for any sourcing. If it's legit, move on.

Once I review what is in ``\drivers\``, I change the query to show me all binaries with different digsig_result:

.. code-block:: console

    > digsig_result:"Bad Signature"  digsig_result:"Invalid Signature"  digsig_result:"Invalid Chain"  digsig_result:"Untrusted Root"  digsig_result:"Explicit Distrust" digsig_result:"Expired"

Some added bonus material, I like to also track ``.sys`` files. Sometimes malicious software will drop it as a ``.sys`` file to bypass detection, or they actual wrote a kernel mode driver.

.. code-block:: console

    > (observed_filename:"c:\windows\system32\" OR observed_filename:"c:\windows\syswow64\") .sys
    > (observed_filename:“c:\windows\syswow64\drivers”) .sys
    > (observed_filename:"c:\windows\system32\drivers\") .sys digsig_sign_time:[* TO 2015-10-01T23:59:59]

Easy, right?

The first two queries identify any sys files in either ``system32`` or ``syswow64``. Begin to also tune your ``digsig_result`` to identify anything odd laying around.
The final query of the 3 highlighted is looking for signing time of the signature (cert). It's an easy way to identify malicious drivers loading with stolen certs from years past. Perhaps, a driver that has been dormant for a long period of time. 

Process
_______

The reason I start with Binary is because it can't lie. What executes, is collected. Now, let's take a peek on the process side.

When an endpoint is exploited either via SMB or IPC, the process chain will begin with ``ntoskrnl.exe``, ``svchost.exe``, or ``lsass.exe``.

.. code-block:: console

    > process_name:ntoskrnl.exe (digsig_result_modload:"Unsigned" OR digsig_result_modload:"Explicit\ Distrust")

Tune this how you like by changing the process name or digsig result. This assists with identifying any suspicious module loads by critical processes on Windows.
If you find a malicious module load via this method, it's highly possible this is a later stage of persistence from the initial delivery. Definitely go back and review all data for the affected endpoint.
