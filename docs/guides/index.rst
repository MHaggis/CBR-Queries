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


.. toctree::
   :maxdepth: 2
   :caption: Contents

   cli
   sysmon
