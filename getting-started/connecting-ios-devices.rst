Connecting iOS devices
======================

Connecting your iOS device
--------------------------

To connect an iOS device, such as an iPhone or iPad, to your Device Hub, follow these steps:

1. Make sure your iOS devices is turned, fully charged and unlocked.
2. Connect your iOS device to your Device Hub using an USB cable.
3. When the *Trust this Device* pop-up appears on your iOS device, click *Trust*. It can take up to one minute
   for your iOS device and Device Hub to initiate the pairing process.
4. On the Device Hub, navigate to http://localhost:17894/ and click the Devices tab. Your
   device is now visible.
5. Click your device, and click *Remote Screen*. You will now see a mirror of the device screen on your PC.

Enabling automation on your iOS device
--------------------------------------

Once your device is connected to your Device Hub, follow these steps to configure your device:

1. Press the *Home* button and then tap *Settings*. Scroll down to and tap *Developer* and check *Enable UI Automation*.
2. Go back to the *Settings* screen and tap *Safari*. Scroll down to the bottom of the page and tap *Advanced*
3. Make sure the *Web Inspector* toggle is enabled.

Prepare your device for continuous automation
---------------------------------------------

You can now fine-tine your device for continuous automation. When your device runs continuously, you want to
make sure your device does not drain the battery and does not automatically lock itself. Both a drained battery
and a locked device would prevent your tests from running on your device.

The main consumer of battery power is your device screen. To configure your screen, perform these steps on
your device:

1. Press the *Home* button and then tap *Settings*. Tap *Display & Brightness*.
2. Set the *Brightness* level to minimal.
3. Set *Auto-Lock* to *Never*.


Troubleshooting iOS device connections
--------------------------------------

If your iOS device does not appear:

1. Run the `lsusb` command in a shell session in your Device Hub. This will list all USB devices which are
   connected to your Device Hub. If you do not see your device in this list, check the USB connection between
   your device and the Device Hub.
2. Run the `idevice_id -l` command in a shell session in your Device Hub. This will list all iOS device
   connected to your Device Hub. If you do not  your device in this list, try unplugging your device and
   connecting your device again.
