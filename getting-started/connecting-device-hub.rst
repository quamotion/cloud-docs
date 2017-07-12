Connecting your Device Hub to your Quamotion Cloud account
==========================================================

To connect your Device Hub to your Quamotion Cloud account, you must start the Device Hub agent and enable
the Device Hub agent in your Quamotion Cloud account.

Starting the Device Hub agent
-----------------------------

We'll temporarily run the Device Hub interactively. 

As a first step, let's grant your user access to Docker:

.. code:: shell

    sudo groupadd docker
    sudo gpasswd -a `whoami` docker
    newgrp docker

Then, let's make sure Docker is configured correctly:

.. code:: shell

    docker run hello-world

Next, configure the application settings for the Device Hub agent:

.. code:: shell

    cp /usr/local/quamotion-monitoring/appsettings.json .

Use your favourite editor and change the value of `dockerEndpoint` to `unix://var/run/docker.sock`

Then, start the Device Hub agent:

.. code:: shell

    /usr/local/quamotion-monitoring/Quamotion.Monitoring.StationManager

The Device Hub agent will now start. You should see a message indicating that a new certificate was created.
When you see this mesasge, stop the Device Hub agent by typing `CTRL+C`.

There will be a `certificate.cer` file in your local folder. You need to upload this certificate to your
Quamotion Cloud account to authorize your Device Hub.

Authorizing the Device Hub
--------------------------

To authorize your Device Hub, follow these steps:

1. Go to your Quamotion Cloud account.
2. Click Device Hubs
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