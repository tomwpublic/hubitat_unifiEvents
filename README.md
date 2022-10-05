# hubitat_unifiEvents

This provides PresenceSensor driver capabilities for Hubitat with UniFi network controllers.  The implementation utilizes the UniFi websocket interface to provide the most timely presence updates without polling the controller

The unifiController driver also implements login and session support for the controller so that other custom queries and attributes can be supported.  There is an option to log all events that occur so that they can be further inspected.


Much of this implementation is based on the work shared here:
* https://ubntwiki.com/products/software/unifi-controller/api
* https://github.com/Art-of-WiFi/UniFi-API-client
* https://github.com/oznu/unifi-events
* https://github.com/NickWaterton/Unifi-websocket-interface

Special thanks to @snell for their collaboration and @Bago for their troubleshooting help.

# Manual Installation instructions:

* In the *Drivers Code* section of Hubitat, add the unifiController and unifiClient drivers.
* In the *Devices* section of Hubitat, add a *New Virtual Device* of type UniFi Controller.
* On the configuration page for the newly created *Device*, enter these details:
    * username and password for your UniFi controller web interface
    * the site name as reflected in the URL of your controller, not the web interface (**this is important**)
        * for example, in *italics*: https<k>://10.0.0.2:8443/manage/site/*default*/dashboard or https<k>://10.10.10.1/network/site/*default*/dashboard
* Determine whether you want to log all incoming events and enable that option if you prefer.
   * Events will show up in the eventStream attribute in real time and will be logged in the event history of the controller device.

# Usage instructions:

* Use `createClientDevice` to create specific network clients to track for PresenceSensor
    * *name* is the display name of the child device.  It does not have a connection to the hostname or other aspects of the client or controller.
    * *mac* should be specific in all lower-case and with colons separating the octets.  Example:  a1:b2:3c:4d:be:ef
* Use the `on` command on a child to allow network connection and `off` to disallow network connection.
    * This is useful for managing whether a specific device can connect to your network.

# Disclaimer

I have no affiliation with any of the companies mentioned in this readme or in the code.
