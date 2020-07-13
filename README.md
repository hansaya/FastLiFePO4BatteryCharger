Fast battery charger designed to work with LifePo4 batteries.

Features
* Selectable battery configuration. Up to 7S.
* Charge management based on temperature. Covers cold and warm conditions.
* Automatic system output selection based on power input conditions.
* No back feeding the input.
* High charging current up to 10A.
* Adjustable max input current limit.
* Adjustable max output current.
* Adjustable charge termination current.
* External enable pin can be used to turn on the charger. This is useful when you want to use the car ignition switch to trigger the charging.

More info at https://www.ti.com/lit/ds/symlink/bq24630.pdf?ts=1594663051247&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FBQ24630

# Disclaimer

**I’m not responsible for any life or property damage. Do your own research and use my design at your own risk.**

# Use case

I currently own an dash cam that can record time lapses while car is parked. This is a great feature and find it to be useful. However this requires the camera to be connected to constant power source. Plugging a camera into car battery permanently will get you a empty battery eventually and will put you on a pickle. Specially if you don’t start the car every day. My solution to this problem is to have an secondary battery pack that powers the camera. 

My requirements:
1) Fast charge the battery within 20min or so. ie within in my daily commute.
2) Battery pack needs to handle the high heat and subzero conditions safely.
3) Runs system like a UPS. No interruptions to the output.
4) High charge cycles so that system would last for a long time.

# Design consideration.
1)	Picked bq24630 ic by TI as the solution to this problem. Which covers all my asks.
2)	Picked LifePo4 battery pack for temperature and charge cycle resiliency. Plus less like to detonate inside the car.
3)	2-layes 1oz board to make PCB house manufacturing cost down.
4)	Went with 3S configuration to keep the battery voltage bellow the input voltage. Bq24630 only a buck converter so it needs some head room.
5)	Keep the battery management work out of this design for simplicity.

# Board files

You can use the zip file within cam/ folder to get the board made by a PCB house. Board can be made with 2layer and 1oz copper. If you have the money for higher copper thickness go for it but not required. 

## Assembling the board

* Do SMT soldering for all parts except for connectors and the fuse holders. 
* Trim pots are not required but recommended if you want to tweak the current settings. If you do select the trim ports, **DO NOT INSTALL R4, R5, R16, R17, R18 and R19.** R4 and R5 is used to set the charging  current, R17 and R17 for termination current and finally R18 and R19 is for adapter current limit. Default values set on schematic designed for 4A adapter current limit, 3A charging current limit and 0.3A termination current.
* NTC thermistor required to let the charger operate at full current. 1.9v at the NTC positive legs could trigger into normal operation mode for testing.
* Add solder to no mask section to increase the current capabilities. This how I got away with 1oz copper.
* R13 and R14 can be used to set the output voltage. Use 1.8(1+R13/R14) to set the voltage. My schematic sets this at 10.8V (LifePo4 3S).
* C11 can be used to set the safety timer. Checkout the datasheet for more information.
* P-CH mosfet I picked are only designed for 20v so do not exceed 20v input voltage.
* LED outputs are not required but handy to have.

# Other considerations

*	Install an external battery protection system between the battery and the charger. 
*	Even though charger can do 10A, inductor seems to get bit toasty at that level of current. I found 6A to be a happy medium. 

# TODO

* Looks like I overlooked the charge enable pin configuration. With the current design, enable pin only enables the charging and output get connected to the input as soon as a valid input is present. I need to use the EN pin to trigger the bypass switch as well.



