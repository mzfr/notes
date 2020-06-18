# Services

Runs code inside the application.

- These are implemented on `onStartCommand()` , this method accepts the intent
    - This could be vulnerable but again it depends on the code like what it is doing actually inside the code. How the intents are handled.
    - `run app.service.start` to start the service and see what's up.
- There is something called `Bound Service` - this help application connect with each other
    - There are ways to implement this but mostly it done by what's know as `Messenger Implementation`
        - Check out `handleMessage()` functions:
            - That will tell you what kinds of message are expected and how the application executes other functions.
- `run [app.service.info](http://app.service.info) -a <package-name>`