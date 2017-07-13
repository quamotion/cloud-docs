Quamotion Cloud API
===================

Quamotion Cloud exposes a REST API which you can use to interact with Quamotion Cloud.

For example, you can programatically access data on Quamotion Cloud and export data to your own in-house systems.

For an overview of the REST API which Quamotion Cloud exposes, click the REST API link in the bottom-left corner of your Quamotion Cloud project.

Authentication
--------------

Quamotion Cloud uses Azure Active Directory and OAuth for authentication. To authenticate yourself with Quamotion Cloud, you will
first need to obtain a JWT token from Azure Active Directory, and then present that token to Quamotion Cloud when you issue a request.

When requesting a token, make sure you specify https://cloud.quamotion.mobi/ as the resource URL, and use https://login.microsoft.com/common
as the authority.

.. warning::

    Please note that the resource URL is ``https://cloud.quamotion.mobi/`` and not ```https://cloud.quamotion.mobi``. Authentication
    with Quamotion Cloud will fail if the resource URL does not include the trailing ``/``.

Python
~~~~~~

When developing scripts in Python, you can use the following sample code to obtain an access token:

.. code:: python

    #!/usr/bin/python3
    import adal

    # It is _super_ important the / is at the end of the URL; it is part of the audience!
    resource = 'https://cloud.quamotion.mobi/'
    client_id = os.environ['AGENT_API_USER']
    client_secret = os.environ['AGENT_API_PASSWORD']
    context = adal.AuthenticationContext('https://login.microsoftonline.com/common')

    token = context.acquire_token_with_client_credentials(resource, client_id, client_secret)
    accessToken = token['accessToken']

Once you have obtained your access token, you can use this access token in the authorization header of your HTTP requests:

.. code:: python

    #!/usr/bin/python3
    import requests

    headers = { 'Authorization': 'Bearer ' + accessToken}
    r = requests.get("http://cloud.quamotion.mobi/api/version", headers=headers)