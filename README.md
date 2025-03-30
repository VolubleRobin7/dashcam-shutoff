# Dashcam Shutoff

## Preamble

I have a *Blackvue DR900X Plus* 2 channel dashcam, paired with a *Blackvue B-130X* battery in my car.
This combination works great, and I can sleep sound knowing that my car battery will never be affected my the recording of my dashcam.
However there are periods of time where my car will not get driven for days while parked at home, and therefore the camera will record in parking mode off the power of the Blackvue battery until it runs out. This is fine, however this means that then if I take a quick 5 minute drive down to the shops, the battery will not charge back up enough for it to stay on while at the shops. I realised it was silly to have it recording while at home, recording nothing of importance, and then not have enough power to record while out, where it is important.

Since Blackvue does not have a geofencing feature within their software to turn off the dashcam while at home. I decided it was necessary to build a device that detects whether it is at home, and cuts the power to the dashcam if so in order to preserve battery power.

## The Device

### Main Components

- **ESP32** - This is the microcontroller for the logic of the project, and is programmed via a ESPHome script.
- **Optoisolator** - To detect whether the accessory power of the car is active (whether the engine is running).
- **MOSFET** - To turn the power to the dashcam on and off.

### Requirements

- If the engine is on, the dashcam must be on no matter what.
- When the dashcam is at home, and the car engine is off, the dashcam should be off.
- When the dashcam is away from home, and the car engine is off, the dashcam should enter parking mode and stay in until either the engine is turned back on or the battery runs out.
- The ESP device should sleep while the engine is off. Leaving it running would waste battery power, and therefore defeat the purpose of turning off the dashcam.
- There should be an override, to tell the device not to turn off the dashcam even if the car is parked at home.
- The completed solution should be able to placed neatly inside the car near the dashcam battery. Loose wiring or easily breakable connections would not stand up to the movements that happen inside a vehicle.

put photos of the device?

## Challenges

1. How would this device control the dashcam? If it is to sit between the battery and the dashcam, it would need to be have the same plugs as the dashcam and battery.
    - A fair amount of research went into finding out what male and female plugs would exactly match the plugs on the battery and the dashcam, and after a fair enough of reverse image searching and checking countless datasheets, I came across the Würth Elektronik power connectors (check DigiKey list). Although I am not sure that these are the *exact* connectors Blackvue used, they for sure are a good match and slot in nicely.
2. The dashcam still needs to retain all its original functionality. 
    - If placing this device inbetween the battery and the dashcam meant that features would be lost, it would not a good project. Testing the voltages and signals from the battery made sure that no data was being transferred from the battery to the dashcam, only power. This meant that the device would not be interupting any signals the dashcam was originally receiving.

## Links

- [DigiKey Part List](DIGIKEY-LIST-LINK) - All the parts that I used in the end to create this device. Although this is all I used, it would be recommended to get extras as spares incase things go wrong during building.

## Credits/References

- [dashcam-parkmode](https://github.com/Swap-File/dashcam-parkmode/tree/master) by Swap-File - A GitHub repo I came across from a [thread](https://www.rdforum.org/threads/99757/) talking about very similar problems to what I have described here, and that project very much formed the basis of my project here now.