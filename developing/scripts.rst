Develop Custom Monitoring Scripts
=================================

You can develop your own scripts which can be used as monitoring scripts in Quamotion Cloud.

Monitoring scripts can be `Python <https://pypi.python.org/pypi/quamotion/>`_ or `PowerShell <https://www.powershellgallery.com/packages/Quamotion.PowerShell/>`_ scripts which automate actions on iOS and Android devices,
using the Quamotion WebDriver. For more information on how to develop scripts, see the Quamotion WebDriver documentation.

When executing in the Quamotion Cloud, your scripts will run inside Docker containers which have the Quamotion packages and their
dependencies pre-installed.

Your script will need to start a WebDriver session, execute actions on the device, and stop the session when done.
You are also responsible for submitting back the results to the Quamotion Cloud.

Interacting with the device
---------------------------

When your script runs in the Quamotion Cloud, you can connect to the Quamotion WebDriver at the usual location - 
that is, http://localhost:17894/. You can use the ``DEVICE_ID`` environment variable to know on which device
you need to create a session.

Submitting back results
-----------------------

You are responsible for submitting back the results to the Quamotion Cloud. You can use the Quamotion Cloud API
to interact with the Quamotion Cloud.

To assist you, the following environment variables are available:

+--------------------------------+---------------------------------------------------------------------------------------------+
| Environent Variable            | Description                                                                                 |
+================================+=============================================================================================+
| ``AGENT_API_URL``              | The URL of the Quamotion Cloud project. For example, http://myproject.cloud.quamotion.mobi  |
+--------------------------------+---------------------------------------------------------------------------------------------+
| ``AGENT_API_TOKEN``            | The JWT token to use when authenticating with the Quamotion Cloud.                          |
+--------------------------------+---------------------------------------------------------------------------------------------+
| ``DEVICE_ID``                  | The ID of the device on which the test is running                                           |
+--------------------------------+---------------------------------------------------------------------------------------------+
| ``SCENARIO_ID``                | The ID of scenario which is running                                                         |
+--------------------------------+---------------------------------------------------------------------------------------------+
| ``GIT_COMMIT``                 | The SHA-1 hash of the git commit of your script                                             |
+--------------------------------+---------------------------------------------------------------------------------------------+
| ``JOB_NAME``                   | An internal name of the job which is currently running.                                     |
+--------------------------------+---------------------------------------------------------------------------------------------+
| ``BUILD_NUMBER``               | An internal ID which uniquely identifies the current monitoring run.                        |
+--------------------------------+---------------------------------------------------------------------------------------------+

Authentication
--------------

When submitting results to Quamotion, you'll need to authenticate. You can use the credentials assigned to the agent on which your
test is running. You receive an access token in the form of the ``AGENT_API_TOKEN`` environment variable. You can then use access
``Authorization: Bearer {accessToken}`` header in your requests to Quamotion Cloud.