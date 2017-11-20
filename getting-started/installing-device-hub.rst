Installing your Device Hub
==========================

Quamotion Cloud allows you to run monitoring scripts on iOS and Android devices. If you want to
host these devices on your premises, you can connect these devices to your Quamotion Cloud project
using a Device Hub.

A Device Hub is a computer or server to which you connect your devices using an USB cable. The Device
Hub then manages the connection between your devices and the Quamotion Cloud.

Currently, the Device Hub runs on any computer running CentOS 7.

.. note::

    Most commands in this section require sudo privileges. If required, either sign in as a root user
    or type ``sudo`` before the command itself.

Installing the Quamotion Software
---------------------------------

These steps will help you install Quamotion Software on your Device Hub.

.. code:: shell

    wget -nv -nc https://download.docker.com/linux/centos/docker-ce.repo -O /etc/yum.repos.d/docker-ce.repo
    wget -nv -nc https://qmrepo.blob.core.windows.net/centos/quamotion.repo -O /etc/yum.repos.d/quamotion.repo
    
    yum install -y epel-release
    yum install -y --nogpgcheck  quamotion-device-hub

    ln -s /lib64/libdl.so.2 /lib64/libdl.so

Updating the Quamotion Software
-------------------------------

Run the following command to update the Quamotion Software:

.. code:: shell

    yum clean all
    yum --nopgpgcheck update

Granting permissions
--------------------

The Quamotion Device Hub uses Docker containers to start agents which can execute scripts on devices. To grant the Quamotion
Device Hub permissions to access Docker, run the following commands:

.. code:: shell

    groupadd docker
    usermod -aG docker quamotion-device-hub

Verifying the Quamotion Software
--------------------------------

The Quamotion WebDriver and Quamotion Device Hub Agent should now be running on your Device Hub. The Quamotion WebDriver
runs as the ``quamotion`` service, whereas the Quamotion Device Hub Agent runs as the ``quamotion-device-hub`` service.

You can check the status of these services through the ``systemctl status`` command:

.. code:: shell

    systemctl status quamotion
    systemctl status quamotion-device-hub

The Quamotion Device Hub Agent uses Docker to run agents. You can test Docker by running this command:

.. code:: shell

    docker run hello-world

Some of the folders the Quamotion WebDriver uses may become unavailable after a reboot. In this case, the Quamotion WebDriver
may fail to start and you may see an access denied error message. In that case, you can manually recreate these folders and
restart the Quamotion WebDriver service:

.. code:: shell

    mkdir /var/run/quamotion
    chown quamotion:quamotion /var/run/quamotion

    mkdir /var/log/quamotion
    chown quamotion:quamotion /var/log/quamotion

    mkdir /var/lib/quamotion
    chown quamotion:quamotion /var/lib/quamotion

    systemctl start quamotion

Some of the folders the Quamotion Device Hub uses may become unavailable after a reboot. In this case, the Quamotion Device Hub
may fail to start and you may see an access denied error message. In that case, you can manually recreate these folders and
restart the Quamotion Device Hub service:

.. code:: shell

    mkdir /var/run/quamotion-device-hub
    chown quamotion-device-hub:quamotion-device-hub /var/run/quamotion-device-hub

    mkdir /var/log/quamotion-device-hub
    chown quamotion-device-hub:quamotion-device-hub /var/log/quamotion-device-hub

    mkdir /var/lib/quamotion-device-hub
    chown quamotion-device-hub:quamotion-device-hub /var/lib/quamotion-device-hub

    systemctl start quamotion-device-hub
