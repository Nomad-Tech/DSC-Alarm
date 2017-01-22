### REST API Setup for a Smartthings App

Requirements:
 Any Web Browser (I use Chrome with json plugin)
 Your Smartthings app OAuth Client ID and Client ID Secret values

Goto the "First URL" below and replace the $client variable at the end of the URL with the actual OAuth client id code from your Smartthings App so it looks something like client_id=4832fdhs-343shfd-fdhjsdn2-sfjkd

First URL:
US    https://graph-na02-useast1.api.smartthings.com/oauth/authorize?response_type=code&redirect_uri=http://localhost&scope=app&client_id=$client
EU    https://graph-eu01-euwest1.api.smartthings.com/oauth/authorize?response_type=code&redirect_uri=http://localhost&scope=app&client_id=$client

Paste the resulting line into your web browser (note it's worthwhile to save all these URLs you are making until it's all setup).
You should see the Smartthings login page, login with your usual developer credentials.

You will now be at an Authorization page, click on the dropdown and select your From: location. Now you need to authorize the Alarm Panel device you created earlier, it should be in the list under "Allow Endpoint to control These Things". Make sure it's selected and then click the "Authorize" button at the bottom.

You will get an error page in your web browser about not being able to connect, this is OK and expected. Look at the URL, it looks something like http://localhost/?code=AAAAAA . We need the code=AAAAAA bit for the next step so copy that down and save it.


In the URL below, replace $client with your OAuth Client ID again and replace $secret with your OAuth Client ID Secret and finally replace $code with the code from above (just the bits after the equal sign so for this example just YdJJS2y).

Second URL:

US    https://graph-na02-useast1.api.smartthings.com/oauth/token?grant_type=authorization_code&scope=app&redirect_uri=http://localhost&client_id=$client&client_secret=$secret&code=$code

EU    https://graph-eu01-euwest1.api.smartthings.com/oauth/token?grant_type=authorization_code&scope=app&redirect_uri=http://localhost&client_id=$client&client_secret=$secret&code=$code

Paste your resulting new Second URL line into the web browser again. If all went well you should see JSON output on the page with a field called "access_token". Copy the access_token value down it looks something like 'a743h22sds-221sahdbabv-sh282hs-sn21712'.

SAVE THAT ACCESS CODE!

You need that everytime you want to send a command to your new Smartthings App!

You now need to get your apps ID so you can reference it directly, go to the URL below and if prompted login with your Smartthings developer id you have been using.

List all your installed apps:

US    https://graph-na02-useast1.api.smartthings.com/api/smartapps/installations/
EU    https://graph-eu01-euwest1.api.smartthings.com/api/smartapps/installations/

Search for a 'label' field matching your application name and copy down the 'id' field right above it.
(It helps if you have a JSON formatted plugin in your web browser but it's just as easy to grab if you don't)

Once that is done, locate the following lines in your alarmserver.cfg and fill them in with the app ID and access token:
callbackurl_app_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
callbackurl_access_token=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
