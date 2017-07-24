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

Installing Docker
-----------------

When Quamotion Cloud runs scripts on your Device Hub, these scripts run in an isolated environment using
Docker containers. In order to run Docker containers, you must install Docker on your Device Hub.

Quamotion Cloud uses the latest Community Edition (CE) version of Docker. Let's install Docker:

.. code:: shell

    yum install -y yum-utils device-mapper-persistent-data lvm2
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    yum makecache fast
    yum install -y docker-ce

    # A quick test to make sure it actually works
    systemctl daemon-reload
    systemctl restart docker
    docker run hello-world

Installing the Quamotion Software
---------------------------------

These steps will help you install Quamotion Software on your Device Hub.

Before we get started, let's install a couple of utilities that can come in handy later:

.. code:: shell

    yum install -y wget # used to download rpm files
    yum install -y unzip # used to unzip the developer disk images
    yum install -y epel-release # This repository contains the android-tools package
    yum install -y usbutils # Contains lsusb, for troubleshooting purposes only

Quamotion Software relies on custom versions of libgdiplus and libimobiledevice. You can acquire these
by installing a custom repository:

.. code:: shell

    # Download updated versions of libimobiledevice, usbmuxd, libgdiplus
    wget -nv -nc http://download.opensuse.org/repositories/home:qmfrederik/CentOS_7/home:qmfrederik.repo -O /etc/yum.repos.d/quamotion.repo

Finally, you can download and install the RPM packages for the Quamotion WebDriver and Quamotion Device Hub:

.. code:: shell

    # Download the Quamotion software
    webdriver_version=0.70.5.11552
    device_hub_version=0.66.106.1713
	wget -nv -nc https://qmcdn.blob.core.windows.net/download/quamotion-webdriver.$webdriver_version.rhel.7.0-x64.rpm -O ~/quamotion-webdriver.$webdriver_version.rhel.7.0-x64.rpm
    wget -nv -nc https://qmcdn.blob.core.windows.net/download/quamotion-device-hub.$device_hub_version.rhel.7.0-x64.rpm -O ~/quamotion-device-hub.$device_hub_version.rhel.7.0-x64.rpm

    yum install -y ~/quamotion-webdriver.$webdriver_version.rhel.7.0-x64.rpm
    yum install -y ~/quamotion-device-hub.$device_hub_version.rhel.7.0-x64.rpm

Verifying the Quamotion Software
--------------------------------

The Quamotion WebDriver and Quamotion Device Hub Agent should now be running on your Device Hub. The Quamotion WebDriver
runs as the ``quamotion`` service, whereas the Quamotion Device Hub Agent runs as the ``quamotion-device-hub`` service.

You can check the status of these services through the ``systemctl status`` command:

.. code:: shell

    systemctl status quamotion
    systemctl status quamotion-device-hub

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