Connecting your Device Hub to your Quamotion Cloud account
==========================================================

To connect your Device Hub to your Quamotion Cloud account, you need to upload the Device Hub certificate to your Quamotion Cloud account to authorize your Device Hub.

Authorizing the Device Hub
--------------------------

To authorize your Device Hub, follow these steps:

1. Retrieve the certificate from your Device Hub. The certificate is located in ``/var/lib/quamotion-device-hub/certificate.cer``. 
   Alternatively, if you are connecting remotely to your device hub, you can download the certificate from http://device-hub:17894/certificate.cer.
2. Go to your Quamotion Cloud account.
3. Click *Hubs* in the top navigation bar.
4. In the *Add a new Device Hub* section, click *Choose File* and navigate to the `certificate.cer` which you
   retrieved from your Device Hub.
5. Click *Upload*

Your Device Hub is now authorized and you can restart the Device Hub agent

Troubleshooting the Device Hub agent
------------------------------------

To get status information for your Device Hub agent, navigate to http://localhost:17895/.