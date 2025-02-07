## **XboxPowerOn.JS**

Xbox One power control via CLI / Node.JS based app (can be run in-browser without downloads too, for example using ```Eruda``` to get access to DevTools on mobile browsers using the ``Chromium`` engine  (``Google Chrome`` / ``Edge`` / ``FreeAdBlockBrowser`` etc...) 

## Installation

to use as CLI program 
```node
npm install -g xbox-on
```
or to use as a module
```node
npm install xbox-on
```

## Usage (CLI)

```node
xbox-on --help

  Usage: cli --ip=<ip_address> --live_device_id=<live_device_id>

  Options:

    -h, --help                             output usage information
    -i, --ip <ip>                          Xbox One IP Address
    -l, --live_device_id <live_device_id>  Xbox One Live Device ID
    -t, --tries <tries>                    Number of times to send power on packet
    -d, --delay <delay_between_tries>      Delay between power packets
```

## Usage (Module)
```node
var Xbox = require('xbox-on');                // Require module
var xbox = new Xbox(ipAddress, liveDeviceId); // Create new xbox

// Optional, defaults shown
var options = {
    tries: 5,
    delay: 1000,
    waitForCallback: false
};

xbox.powerOn(options);                        // Issue power on command
```

## Getting your Xbox One's IP address

On your Xbox, go to Settings > Network > Network Settings > Advanced Settings

## Getting your Live ID

On your Xbox, go to Settings > System > Console info & updates and look under "Xbox Live device ID"

## Caveats

Since dgrams are effectively synchronous and don't rely on a response, we can usually just fire them off and not worry
about the callbacks.  However, there are cases where you might want to wait until the final packet is sent before
proceeding.  In this case, you might want to pass the `waitForCallback` option to the `powerOn` call to ensure that all
requests are sent before continuing.  The CLI is an obvious use case for this, as terminating prior to callback wouldn't
send any packets at all!
