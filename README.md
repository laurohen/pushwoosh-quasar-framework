# pushwoosh-quasar-framework
Receive pushwoosh notifications using Quasar framework / vue.js



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

      appid: "XXXXX-XXXXX",

      projectid: "XXXXXXXXXXXXX", 

      //serviceName: "MPNS_SERVICE_NAME" 


    });


    pushwoosh.registerDevice(
       function(status) {

       var pushToken = status.pushToken;
        alert('Value token device : ' + pushToken)

       // handle successful registration here
    },
    function(status) {

        alert('Error register : ' + status)
         // handle registration error here
      }
    );
    
  } , false)
    
}      


     

