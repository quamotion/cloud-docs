Connecting your Device Hub to your Quamotion Cloud account
==========================================================

To connect your Device Hub to your Quamotion Cloud account, you must start the Device Hub agent and enable
the Device Hub agent in your Quamotion Cloud account.

Starting the Device Hub agent
-----------------------------

We'll temporarily run the Device Hub agent interactively. 

First, make sure the Device Hub agent is not running as a SystemD service:

.. code:: shell

    systemctl stop quamotion-monitoring
    systemctl disable quamotion-monitoring

Next, let's grant your user access to Docker:

.. code:: shell

    groupadd docker
    gpasswd -a `whoami` docker
    newgrp docker

Then, let's make sure Docker is configured correctly:

.. code:: shell

    docker run hello-world

Next, configure the application settings for the Device Hub agent:

.. code:: shell

    cp /usr/share/quamotion-monitoring/appsettings.json .

Use your favourite editor to open the ``appsettings.json`` file and change the value of ``dockerEndpoint`` to ``unix://var/run/docker.sock``

Then, start the Device Hub agent:

.. code:: shell

    /usr/share/quamotion-monitoring/Quamotion.Monitoring.StationManager

The Device Hub agent will now start. You should see a message indicating that a new certificate was created:

.. code::

    info: Quamotion.Monitoring.Common.MonitoringClient[0]
          Creating a new authentication certificate. You will need to trust this certificate first before this server can log on.
    info: Quamotion.Monitoring.Common.MonitoringClient[0]
          Successfully created a new authentication certificate.

followed by multiple messages indicating the Device Hub is not authorized:

.. code::

    info: Quamotion.Monitoring.Common.MonitoringClient[0]
          This device hub is not authorized. Waiting.

When you see this mesasge, stop the Device Hub agent by typing `CTRL+C`.

There will be a ``certificate.cer`` file in your local folder. You need to upload this certificate to your
Quamotion Cloud account to authorize your Device Hub.

Authorizing the Device Hub
--------------------------

To authorize your Device Hub, follow these steps:

1. Go to your Quamotion Cloud account.
2. Click *Hubs* in the top navigation bar.
3. In the *Add a new Device Hub* section, click *Choose File* and navigate to the `certificate.cer` which you
   retrieved from your Device Hub.
4. Click *Upload*

Your Device Hub is now authorized and you can restart the Device Hub agent

Restarting the Device Hub agent
-------------------------------

To restart the Device Hub agent, run the following command:

.. code:: shell

    /usr/local/quamotion-monitoring/Quamotion.Monitoring.StationManager

You will now see a message indicating that the Device Hub agent has connected successfully to Quamotion Cloud.

Troubleshooting the Device Hub agent
------------------------------------

To get status information for your Device Hub agent, navigate to http://localhost:17895/.