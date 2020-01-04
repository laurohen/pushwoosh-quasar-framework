# pushwoosh-quasar-framework
Receive pushwoosh notifications using Quasar framework / vue.js

Open a new project in Quasar Framework

# Node.js >= 8.9.0 is required.

    $ yarn global add @quasar/cli
# or
    $ npm install -g @quasar/cli

    $ quasar create <folder_name>

Note:
iOS Simulator can neither subscribe nor receive push notifications. Android and Windows Phone emulator will work.
To integrate Pushwoosh with your Cordova application, follow these simple steps:

1. Install the Plugin source code into your app:

For Cordova: 

    cordova plugin add pushwoosh-cordova-plugin

2. Whitelist .pushwoosh.com domain in the config.xml file:

    <access origin="*.pushwoosh.com" />

Do not forget to add cordova-plugin-whitelist plugin for android platform.

    cordova plugin add cordova-plugin-whitelist

3. Get the google-services.json from your Firebase console as described here and add it to your project.


4. Add the following section to your config.xml:

    <platform name="android">
       <resource-file src="google-services.json" target="app/google-services.json" />
       ...
    </platform>



The first step is always to generate a new plugin using Quasar CLI:

    $ quasar new boot 'file-name'

Where 'file-name' should be exchanged by a suitable name for your boot file.

This command creates a new file: /src/boot/<name>.js with the following content:
  
In the quasar.conf.js file add:

boot: [

'file-name'

],


In the boot file that was generated add the code below:



// "async" is optional

    export default async ({ store }) => {  
  
    document.addEventListener('deviceready', () => {

     

    var pushwoosh = cordova.require("pushwoosh-cordova-plugin.PushNotification");

    // Should be called before pushwoosh.onDeviceReady
    document.addEventListener('push-notification', function(event) {

            var notification = event.notification; 
            alert(notification)
            // handle push open here
    });


    // Initialize Pushwoosh. This will trigger all pending push notifications on start.
    pushwoosh.onDeviceReady({
        
        //PUSHWOOSH_APP_ID
      appid: "XXXXX-XXXXX", 
      
        //YOUR_FCM_SENDER_ID
      projectid: "XXXXXXXXXXXXX", 

      //serviceName: "MPNS_SERVICE_NAME" 


    });


    pushwoosh.registerDevice(
       function(status) {

       var pushToken = status.pushToken;
        alert('Value token device : ' + pushToken)
       //The token device shown in Alert is what you will use to send panel notification or Api Pushwoosh
       
       // handle successful registration here
    },
    function(status) {

        alert('Error register : ' + status)
         // handle registration error here
      }
    );
    
    } , false)
    
    }      


### Finally generate .apk and subscribe to the App.

### Install on the phone and the first run of the App will generate a unique token id on Pushwoosh of that phone.

### Ready !!! 

### You can now test through the Pushwoosh website panel or send via Pushwoosh Api using the generated token id

     

