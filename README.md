# SmartThings Repo

This is an adaptation/modification from LXXero's GitHub https://github.com/LXXero/DSCAlarm

## Alarmserver Instructions

### Setup device handlers

Using the Smartthings IDE create the new device handlers using the code from the devicetypes directory.

There are 6 types of devices handlers you can create:

* DSC Stay Panel  - (Shows partition status info and provides Stay switch that can be used in routines)
* DSC Away Panel  - (Shows partition status info and provides Away switch that can be used in routines)
* DSC Zone Contact - (contact device open/close)
* DSC Zone Motion  - (motion device active/inactive)
* DSC Zone Smoke - (wireless/4-wire smoke device, detected/clear/test. It's nearly the same as motion or contact, as it's attached to a zone.)
* DSC Zone CO - (wireless/4-wire carbon monoxide device, detected/clear/test. It's similar to DSC Zone Smoke.)

At a minimum you'll probably want the Stay/Away panels, Contact, and Motion.

In the Web IDE for Smartthings create a new device type for each of the above devices and paste in the code for each device from the corresponding groovy files in the repo. Alternatively, setup github integration, create a new github repository with "Nomad-Tech" as owner, "DSC-Alarm" as name, and "master" as branch. Once you have setup this repo, you can easily add all the devices. Be sure to check the publish checkbox at the bottom.

For all the device types, make sure publish them. If you're using github, use the "publish" checkbox. If you forget, or installed the code manually via copy/paste, you'll have to go into each one and click "publish -> for me" again.

### Smartapp Setup

1. Create a new Smartthings App in the IDE. Use the code from DSCIntegration.groovy in the smartapps folder for the new smartapp. Save and publish.

2. Click "Enable OAuth in Smart App" and copy down the generated "OAuth Client ID" and the "OAuth Client Secret", you will need them later to generate an access code.
Make sure you save and apply this before you leave the page, as the oauth information displayed isn't actually applied until you do so.

3. Now the hard part, we need to authorize this Smarttthings app to be used via the REST API.
   It's going to take a few steps but all you need is a web browser and your OAuth ID's from the above app setup page.
   Follow the RESTAPISetup.md document in this same repo to finish the setup.

4. Once OAuth setup is completed, edit the settings for the DSC Integration app on your phone, and fill in the IP/Port with the correct information for your alarmserver (Raspberry Pi IP address).
   The port is typically the "httpsport" setting in your alarmserver.cfg, and the IP should be the IP of your alarmserver (Raspberry Pi) and not your envisalink device. If need be, setup any push notifications here as well.
   NOTE: THIS MUST BE THE IP ADDRESS! THE CODE DOES NOT RESOLVE HOSTNAMES/DNS AT THIS TIME. See TODO.

### Alarmserver Setup

1. First, edit 'alarmserver.cfg' and add in the OAuth/Access Code information to the callback_url_app_id and callbackurl_access_token values, and edit your zones/partitions at the bottom of the file.

2. The alarm panels and zone devices get created/deleted automatically when alarmserver starts. Ensure all your zones and partitions are properly defined as per the included alarmserver.cfg example.

3. Fire up the AlarmServer. Your devices should get created in smartthings, and you should start seeing events pushed to them within a few moments on your smart phone.

## Thanks!
Thanks goes out to the following people, without their previous work none of this would have been possible:
* juggie
* Ethomasii
* Rob Fisher <robfish@att.net>
* Carlos Santiago <carloss66@gmail.com>
* JTT <aesystems@gmail.com>
* Donny K <donnyk+envisalink@gmail.com>
* Leaberry <leaberry@gmail.com>
* Kent Holloway <drizit@gmail.com>
* Matt Martz <matt.martz@gmail.com>

