# Zword_ZwiftRide-to-BLE-Keyboard
A ESP32 based project to convert button presses on the Zwift Ride controller into BLE keyboard presses. It auto connects to the Zwift RIDE controller and advertises as BLE Keyboard. No other controllers are supported since they use encrypted messages and I din't want to dig in that deep. 


The setup as in the code is made to work with the "MyWoosh" app.
As there are limited keyboard shortcuts available I decided to assign media buttons to the left controller.
I ignored the "paddle" as I couldn't think of any use.

The code is not refactored and completely not-optimized but works fine for me and my purposes. 
There is not much error handling involved.
The hardware that I used is a Lolin D32 Pro.

Via serial-monitor you can read along all important actions while operating if you want to.

# Establish Connection
Don't turn on your trainer or any training app. We want to prevent the controller pairing to something else.

Only the very first time or if you want to connect the hardware to a new PC/Tablet/Phone:
  1) On your PC/Tablet/Phone go to bluetooth settings and connect to "Zword". Allow it to pair.
  (it may show two times as being connected... I have no idea why and I don't bother).
  2) Unplug the ESP32.

For normal usage:
  1) Turn on the LEFT Zwift Ride controller, it should start flashing blue
  2) Power on the ESP32
  3) Wait until the LEFT Zwift Ride vibrates (connection successfully established)
     If the controller vibrate twice after the first one it means the keyboard is also connected
  4) Turn on the RIGHT controller. It will flash blue until it lights up constantly blue
  5) You're ready to go! (Start your favorite cycling app)

# Button assignments:
Left controller:
  - All side buttons:   Shift Down
  - power:              Play/Pause
  - Left/Right:         prev./next track
  - Up/Down:            Volume up/down

Right controller:
  - All side buttons:   Shift Up
  - A:                  Hello Emote
  - Y:                  Hide/Show UI
  - B:                  Battery Low Emote
  - Z:                  Thumbs Up Emote
  - power:              Pause/Resume the ride

# Needed Libraries
https://github.com/T-vK/ESP32-BLE-Keyboard

Depending on when you try to built the sketch, you may want to apply a fix to the library code as described here
(https://github.com/T-vK/ESP32-BLE-Keyboard/issues/313):
Zer0TheObserver on Sep 9, 2024

hat's all you need to do:
1, Open BleKeyBoard.ccp in the ESP32_BLE_Keyboard lib
2, change "hid->manufacturer()->setValue(deviceManufacturer);" TO "hid->manufacturer()->setValue(String(deviceManufacturer.c_str()));"

3, change "BLEDevice::init(deviceName);" TO "BLEDevice::init(String(deviceName.c_str()));"
Run it again.

# Note of thanks
Special thanks to:
- cagnulein with his amazing Qdomyos-Zwift application (https://github.com/cagnulein/qdomyos-zwift?tab=coc-ov-file)
- ajchellew with his zwiftplay project (https://github.com/ajchellew/zwiftplay) and the very good descriptions
- Makinolo for the great work and blog articles on the zwift hardware (https://www.makinolo.com/blog/2024/07/26/zwift-ride-protocol/)
- Jonasbark with his swiftcontrol app (https://github.com/jonasbark/swiftcontrol/tree/main)

All are very good ressources and help to understand how it all works together.

# Ideas for further improvements (most likely will not happen by me...)
- Refactor code and find a better solution for the media key handling
- Include a webservice on the device that lets the user configure the button mapping without changing the source
- Incorporate the padles (if there are any useful things that can be done with it
- Expand MyWoosh shortkeys if they ever decide to extend what they have

# Disclaimer
Use at your own risk. I don't own any rights of the Names "Zwift" and "MyWoosh"


