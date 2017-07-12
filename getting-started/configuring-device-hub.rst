Configuring your Device Hub
===========================

For your Device Hub to be able to run any tests, you must first configure your Device Hub
and then connect devices to it.

To configure your device hub, you must:

- Install a Quamotion License on your device hub
- Install the Developer Disk images if you are going to run tests on iOS devices
- Install a Developer profile if you are going to run tests on iOS devices


Installing a Quamotion License
------------------------------

Quamotion License unlock the full potential of the Quamotion Software on your Device Hub.

To install a license, follow these steps:

1. On your Device Hub, navigate to http://localhost:17894/. Alternatively, navigate to http://device-hub:17894/
   from another computer, where `device-hub` is the IP address of your device hub.
2. Click the Request Trial License link which will take you to the Quamotion website where you can request a Trial
   license.
3. Complete the requested information, and click the Request License link. You will receive a two-week license
   for your Device Hub by e-mail.
4. Once you've received your license file, navigate to http://device-hub:17894/, click *Settings*  and click
   *Install License*.
5. Upload the license file you've received and click *OK*.
6. Finally, restart the Quamotion WebDriver by running

    .. code:: shell

        systemctl reload quamotion

Installing the Developer Disk images
------------------------------------

When Quamotion Cloud runs tests on an iOS device, it uses some of the Apple Developer tools to perform automation tasks.
Examples of such tasks include installing or launching an application, and capturing screenshots.

These tools are not installed on iOS devices by default. They can be added to the iOS device by mounting the
Developer Disk. If you run your app on a device using XCode, XCode mounts the developer disk for you.

Quamotion can mount the developer disk for you, but you need to install the iOS Developer Disk on your 
Device Hub before Quamotion can mount it.

To install the iOS Developer Disk on your Device Hub, you need to download it from a Mac machine
 and copy it to your Device Hub. Follow these steps:

 
1. On a Mac machine, make sure the latest version of XCode is installed
2. Navigate to the ``/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport`` folder
   and create a zip archive that contains the contents of this folder.
3. Copy this zip archive to your Device Hub.
4. Unzip this archive into ``/var/lib/quamotion/devimg/``

Installing a Developer Profile
------------------------------

For you to be able to run the Quamotion Cloud software on your iOS device, the Quamotion Cloud software
needs to be signed with a developer profile which allows the Quamotion Cloud software to run on your device.

In order for you to be able to sign an iOS application, you need to enroll into the
`Apple Developer Program <https://developer.apple.com/programs/enroll/>`.

Once you are an active member of the Apple Developer Program, you can create developer profiles.
A developer profile contains a certificate, which identifies you as the person who signed the application,
as well as a provisioning profile, which lists all the devices that you can install your application on.
Apple limits the number of devices you can test on to 100.

You can export your Developer Profile from Xcode as a `.developerprofile` file. Then,

1. On your Device Hub, navigate to http://localhost:17894/. Alternatively, navigate to http://device-hub:17894/
   from another computer, where `device-hub` is the IP address of your device hub.
2. Click *Settings* and click *Import Developer Profile*
3. Provide the `.developerprofile` package you've created earlier, as well as the password you provided
   when you exported the developer profile and click *OK*.