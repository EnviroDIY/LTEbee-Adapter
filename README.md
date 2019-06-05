EnviroDIY LTE Bee Adapter
==============
The EnviroDIY LTE Bee Adapter shield is an interface board designed to enhance the functioning and stability of the [Digi XBee3 Cellular LTE-M/NB-IoT](https://www.digi.com/products/embedded-systems/cellular-modems/xbee3-cellular-lte-m-nb-iot) radio modules with the [EnviroDIY Mayfly Logger versions 0.5b](https://github.com/EnviroDIY/EnviroDIY_Mayfly_Logger) or earlier.

The two main benefits of the LTE adapter board are:
- additional features for power supply, stability and switching
- status LED lights 

The power benefits are provided via a direct JST connector to the battery, similar to Sodaq GPRSbee modules, and a capacitor chain. Power is thus much smoother, and the XBee module should not brown out and stop communicating.

If using a Mayfly v0.5b, you'll want to make sure that the SJ13 solder jumper is in the configuration where pin 1 of the 
Mayfly bee header is powered by the 3.3Vcc and not directly to the LiPo.  This way, the Mayfly's bee socket only gets power whenever the Mayfly is turned on, and the LTEbee module doesn't wake up when the Mayfly is off (which is what it does if directly connected via SJ13).  

You can then control the bee module's sleep behavior with the sleep pin similar to what we do with the Sodaq GPRSbee radio modules.   

We also have access to the LTE module's reset pin now. If using the Mayfly and the ModularSensors library, the user can thus can set the reset pin to pin 20 in the constructor for the modem in the code sketch. Currently the only time that feature is used, though, is in transparent mode if it doesn’t reply after 4 attempts to enter command mode.  In watching the debugging logs, we haven’t seen it use that reset yet. 

The LTE Bee Adapter shield also has a second solder jumper for selecting how you power the load switch for the Vcc pin of the module.  The default setting is that the LTE module is always powered when the Mayfly bee socket Vcc pin (pin 1) is on.   But if you switch the jumper to the other position, it allows you to turn on and off the power to the LTEbee by using pin 15 of the Mayfly bee socket, which goes to the Mayfly's SJ7 solder jumper.  SJ7 was originally designed to allow you to connect Mayfly pin A5 to either the RingIndicator pin (20) or the Assoc pin (15).   It's a feature we've never used, but we put it on there anyway.  So if you jumper Mayfly SJ7 between the A5 and ASSOC pads, you are then connecting A5 to the Mayfly bee socket pin 15, which goes to SJ1 on the LTEbee_adapter, allowing you to turn on or off the LTEbee by setting A5 high or low.  We aren't sure anyone would want to do that -- since Digi recommends leaving power to the LTEbee on all the time and then command it to sleep using the sleep in (9), rather than yanking power away from it whenever you want to turn it off -- but we added this feature to give us flexiblity in the future.


MORE INFORMATION COMING SOON.


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

