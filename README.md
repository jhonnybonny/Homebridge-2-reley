# Homebridge-2-reley
.ino for Homebridge Http 

NodeMcu Esp8266 Homebridge Switch

Introduction

This will give you a quick and easy way to add a NODEMCU to Apple's HomeKit on an iOS device. It opens up all sorts of possibilities including Scripts running on the server, combined with Apples HomeKit "Scenes", it makes for a powerful combo!

This is by no means a complete solution or ready for long term use but it demonstrates what's possible with a bit more work :)

What's needed:

NODEMCU ( ESP8266 Module )
Raspberry Pi or some other server
Solid State Relay or Normal relay with control circuit
Bread board - optional
Project Box
iOS device
Extension Lead to carve up
Installation

Step 1: Setup the Server

This project requires the use of a server to run the HomeBridge software. I used a Raspberry Pi as I had it readily available but in theory anything that can run Node.Js should work!

You can follow this guide here to get this up and running on a Raspberry Pi.

https://github.com/nfarina/homebridge/wiki/Running-HomeBridge-on-a-Raspberry-Pi

Once installed you need install a plugin and customise the config.json file

Step 2: Config and Plugins

Open your config.json file which should be in ~/.homebridge/config.json using your favourite text editor and add the following

{

"bridge": {

"name": "Homebridge",

"username": "CC:22:3D:E3:CE:30",

"port": 51826,

"pin": "031-45-154"

},

"platforms": [

],

"accessories": [

{

"accessory": "Http",

"name": "Living Room Lamp",

"on_url": "http://NODEMCU_IP:80/LED=ON",

"off_url": "http://NODEMCU_IP:80/LED=OFF",

"http_method": "GET"

}

{

"accessory": "Http2",

"name": "Living Room Lamp",

"on_url": "http://NODEMCU_IP:80/LED1=ON",

"off_url": "http://NODEMCU_IP:80/LED1=OFF",

"http_method": "GET"

}

]

}
You will also need to install the homebride-http plugin. The HomeBridge software will make HTTP GET requests to the NODEMCU which will then turn the Solid State Relay on or off. The call looks like this:

http://NODEMCU_IP:80/LED=ON

http://NODEMCU_IP:80/LED=OFF
To install the plugin type:

sudo npm install homebridge-http or sudo npm install -g homebridge-http
