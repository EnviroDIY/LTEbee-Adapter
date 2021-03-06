EnviroDIY LTE Bee Adapter
==============
The EnviroDIY LTE Bee Adapter shield is an interface board designed to enhance the functioning and stability of the [Digi XBee3 Cellular LTE-M/NB-IoT](https://www.digi.com/products/embedded-systems/cellular-modems/xbee3-cellular-lte-m-nb-iot) radio modules with the [EnviroDIY Mayfly Logger versions 0.5b](https://github.com/EnviroDIY/EnviroDIY_Mayfly_Logger) or earlier.

The [EnviroDIY LTE Bee Adapter shield can be purchased at Amazon.com](https://www.amazon.com/Stroud-Water-Research-Center-EnviroDIY/dp/B07TRHHMDJ).

The two main benefits of the LTE adapter board are:
- additional features for power supply, stability and switching
- status LED lights 

| <img src="https://github.com/EnviroDIY/LTEbee-Adapter/blob/master/doc/images/LTEbee_adapter_front_top.jpg"  height="240"> 
| <img src="https://github.com/EnviroDIY/LTEbee-Adapter/blob/master/doc/images/LTEbee_adapter_back_top.jpg"  height="240"> 
| <img src="https://github.com/EnviroDIY/LTEbee-Adapter/blob/master/doc/images/LTEbee_adapter_right2.jpg"  height="240"> 
| <img src="https://github.com/EnviroDIY/LTEbee-Adapter/blob/master/doc/images/LTEbee%2BMayfly.jpeg"  height="240"> |

The power benefits are provided via a direct JST connector to the battery, similar to Sodaq GPRSbee modules, and a capacitor chain. Power is thus much smoother, and the XBee module should not brown out and stop communicating.  Use a JST jumper wire to connect the LTEbee adapter board to the spare LIPO jack on the Mayfly board.

There are 3 colored LEDs on the LTEbee adapter.
- ON (white) light comes on anytime the LTEbee is awake.
- ASSOC (blue) light is connected to the ASSOC pin of the bee module, and will blink different patterns to show the connection status to the network.
- RSSI (orange) light is the received signal strength indicator.  It will turn on when connecting with the network vary in brightness depending on signal strength. 

DO NOT UNPLUG the LTEbee Adapter board while any of the lights are on, as this might permanently lockup your Digi radio module. Powering down the Mayfly should put set the LTEbee Adapter to put the radio into sleep mode, and this might take a minute or so after turning the Mayfly off. 

If using a Mayfly v0.5b, you'll want to make sure that the SJ13 solder jumper is in the configuration where pin 1 of the 
Mayfly bee header is powered by the 3.3Vcc and not directly to the LiPo (this is the default jumper setting).  This way, the Mayfly's bee socket only gets power whenever the Mayfly is turned on, and the LTEbee module doesn't wake up when the Mayfly is off (which is what it does if the LiPo is directly connected to bee pin 1 via SJ13).  You can then control the LTEbee module's sleep behavior with the module's pin 9 sleep pin (using Mayfly D23).

We also have access to the LTE module's reset pin now. If using the Mayfly and the ModularSensors library, the user can set the reset pin to Mayfly pin 20 in the constructor for the modem in the code sketch. Currently the only time that feature is used, though, is in transparent mode if it doesn’t reply after 4 attempts to enter command mode.  In watching the debugging logs, we haven’t seen it use that reset yet. 

The LTEbee Adapter shield also has two a solder jumper's on the back, giving the user configuration options.

The LTEbee Adapter's **SJ1 solder jumper** allows the user to select how to power the load switch for the Vcc pin of the module.  
- The default setting is that the LTE module is always powered when the Mayfly bee socket Vcc pin (pin 1) is on (as mentioned above).
- If you switch the jumper to the other position (Mayfly A5), it allows you to turn on and off the power to the LTEbee by using pin 15 of the Mayfly bee socket, which goes to the Mayfly's SJ7 solder jumper:  
  - [Mayfly SJ7](https://github.com/EnviroDIY/EnviroDIY_Mayfly_Logger#solder-jumper-connections) was originally designed to allow you to connect Mayfly pin A5 to either the RingIndicator pin (Bee 20) or the Assoc pin (Bee 15). The default is not connected to either (all pads open).
  - If you solder the Mayfly SJ7 jumper between the A5 and ASSOC pads, you are then connecting A5 to the Mayfly bee socket pin 15, which goes to SJ1 on the LTEbee_adapter, allowing you to turn on or off the LTEbee by setting A5 high or low.  We aren't sure anyone would want to do that -- since Digi recommends leaving power to the LTEbee on all the time and then command it to sleep using the sleep pin (Bee 9), rather than yanking power away from it whenever you want to turn it off -- but we added this feature to give us flexiblity in the future.

The LTEbee Adapter's **SJ2 solder jumper** is for selecting which pin on the Bee modules gets connected to Mayfly D19 (Mayfly bee header pin 12).  The default setting is for the LTEBee module's pin 13 to be connected to Mayfly D19, which is how this adapter should always be used with a Digi LTEbee, but changing SJ2 to the other setting will connect pin 12 of the bee module to D19.  This was done in case other manufacturers use the same pinout as the GPRSbee boards, which are different than the Digi LTEbee.


## License
Hardware designs shared are released, unless otherwise indicated, under the [CERN Open Hardware License 1.2](https://www.ohwr.org/projects/cernohl/wiki) (CERN_OHL).

Documentation is licensed as [Creative Commons Attribution-ShareAlike 4.0](https://creativecommons.org/licenses/by-sa/4.0/) (CC-BY-SA) copyright.

## Credits
[EnviroDIY](http://envirodiy.org/)™ is presented by the Stroud Water Research Center, with contributions from a community of enthusiasts sharing do-it-yourself ideas for environmental science and monitoring.

[Shannon Hicks](https://github.com/s-hicks2) is the primary developer of this hardware, with input from many other contributors.

This project has benefited from the support from the following funders:

* William Penn Foundation
* US Environmental Protection Agency (EPA)
* National Science Foundation, awards [EAR-0724971](http://www.nsf.gov/awardsearch/showAward?AWD_ID=0724971), [EAR-1331856](http://www.nsf.gov/awardsearch/showAward?AWD_ID=1331856), [ACI-1339834](http://www.nsf.gov/awardsearch/showAward?AWD_ID=1339834)
* Stroud Water Research Center endowment

