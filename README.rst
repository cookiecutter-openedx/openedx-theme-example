mooc.academiacentral.org
------------------------
.. image:: https://img.shields.io/badge/hack.d-Lawrence%20McDaniel-orange.svg
     :target: https://lawrencemcdaniel.com
     :alt: Hack.d Lawrence McDaniel

This is the custom theme for the Open edX platform `mooc.academiacentral.org <https://mooc.academiacentral.org>`_.
For more information on the structure of this repository please see:

.. _Open edX Custom Theming Tutorial: https://blog.lawrencemcdaniel.com/open-edx-custom-theming-tutorial/
.. _Open edX Official Custom Theming Documentation: https://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/configuration/changing_appearance/theming/create_theme.html

Note that this repository is private and therefore requires the use of Deployment Keys, `located here <https://github.com/academiacentral-org/edx-theme/settings/keys>`_. 
For more information about adding / modifying GitHub deployment keys see `Generating a new SSH key and adding it to the ssh-agent <https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent>`_.
Deployment keys are typically created inside the .ssh folder of the destination Linux server.

Usage
-----
This repository is automatically cloned to edxapp servers during reboots / startups. 

.. code-block:: bash

    crontab -e

You'll find the following two cron entries. The first command clones this repository for the sole
purpose of extracting the bash scripts located in home/ubuntu/edx.scripts and copying these to the
same folder location on the edxapp server on which this cron job is running. The second script 
executes one of these bash scripts, edx.platform-autostart.out, that in turn calls any other scripts
that should execute during reboots. These typically inclue edx.install-config.sh and edx.install-theme.sh
but others could be added for patch and mainentance purposes.

.. code-block:: bash

    @reboot /home/ubuntu/edx.install-scripts.sh > /home/ubuntu/edx.install-scripts.out
    @reboot /home/ubuntu/edx.scripts/edx.platform-autostart.sh > /home/ubuntu/edx.platform-autostart.out




Making Changes to the Open edX Theme
------------------------------------
html files located in folders named "template" are Django Mako template files that are interpretted at run time. It is not necessary to restart the Open edX when modifying these files.
Any files located in "static" require both Asset Compilation as well as a restart of the Open edX application (LMS, CMS, Ecommerce) in which they are stored.

As a highly-preferred alternative to hosting static assets on the edxapp servers you are encouraged instead to leverage the CDN located at `s3://mooc.academiacentral.org <https://s3.console.aws.amazon.com/s3/buckets/mooc.academiacentral.org?region=us-east-1&tab=objects>`_.
Files stored to the CDN become available immediately and require neither Asset Compilation nor a restart of the Open edX platform.