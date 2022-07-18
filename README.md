
## Javascript Events ADA Widget

### Widget Javascript events
By default the widget sends postmessage notification events to the parent frame by using the specified url_done_message in the initialization parameters. Depending on the business logic you can implement second actions when an event is triggered, for example a redirection to a success landing ```cdc:apiwidgetLoginComplete:done``` is fired.

Notifications format:

``` 'cdc:' + process + ':' + result ```

The main javascript events are:

```cdc:apiwidgetLoginComplete:done``` Triggered when the user completes the aggregation

```cdc:apiwidgetLoginComplete:fail``` Trigegred when the aggregation fails


### Example:

```javascript
  var eventMethod = window.addEventListener ? "addEventListener" : "attachEvent";
  var eventer = window[eventMethod];
  var messageEvent = eventMethod == "attachEvent" ? "onmessage" : "message";
  eventer(messageEvent, function (e) {            
    console.log('parent received message!:  ',e.data);
    if(e.data === 'cdc:apiwidgetLoginComplete:done'){
      window.location.href = "https://www.google.com"
    }
  }, false);

```

### List of events available

Aggregation process


|  STEP| VIEW |POSTESSAGE|DESCRIPTION|
|--|--|--|--|
|1|Widget initial load|cdc:initwidget:done|Widget initial load successful|
|2|Widget initial load|cdc:initwidget:fail |Widget initial load failed | 
|3|Accept terms and conditions|cdc:termAndConditionBtn:acepted|Click on the button to ```aeptar``` terms and conditions|
|4|Accept terms and conditions|cdc:termAndConditionBtn:cancel|Click the button to ```cancelar``` terms and conditions|
|5|Send api widget ```accpet term and condition```|cdc:apiwidgetAccept:done|Successful reception of the request to start the process ```/v1/ada/apiwidget/accept/```|
|6|Send api widget ```accpet term and condition```|cdc:apiwidgetAccept:fail|Unsuccessful reception of the request to start the process  ```/v1/ada/apiwidget/accept/```|
|7|Send api widget ```get banks```|cdc:apiwidgetBank:done|Successful receipt of sources request ```/v1/ada/apiwidget/banks/```|
|8|Send api widget ```get banks```|cdc:apiwidgetBank:fail|Unsuccessful reception of soruces request ```/v1/ada/apiwidget/banks/```|
|9|Click button login|cdc:loginBtn:acepted|Click on the button to ```aceptar``` sending credentials|
|10|Click button login|cdc:loginBtn:back|Click on the button to ```volver``` from sending credentials|
|11|Send api widget ```send login```|cdc:apiwidgetLogin:done|Successful receipt of credentials ```/v1/ada/apiwidget/login/```|
|12|Send api widget ```send login```|cdc:apiwidgetLogin:fail|Failed reception of credentials ```/v1/ada/apiwidget/login/```|
|13|Send api widget ```send login```|cdc:apiwidgetLogin:step|Receive second factor authentication ```/v1/ada/apiwidget/login/```|
|14|Send api widget ```send login complete```|cdc:apiwidgetLoginComplete:done|Successful reception at the end of the process ```/v1/ada/apiwidget/login-complete/```|
|15|Send api widget ```send login complete```|cdc:apiwidgetLoginComplete:fail|Failed reception at the end of the process ```/v1/ada/apiwidget/login-complete/```  |
