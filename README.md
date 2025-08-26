"11_sp7etd firmware update manual"

GENERAL NOTES:

NOTE 1: Firmware originated from v6.3.1 Arduino sketch. For use with original ILI9341 320x240 TFT display.

NOTE 2: Flashing ubitx is easy - find tutorials in the net. Short instruction at the end of this README file. To be on the safe side You can buy new arduino nano without gold-pins soldered and solder them to have pins on the same side as usb connector. 

NOTE 3: Mind to rename unpacked directory eg. "ubitxv6-11_sp7etd-ubitx_v6-11_sp7etd" to the same name as *.ino file (eg. "ubitx_v6_11_sp7etd").

NOTE 4: Remember to perform FULL calibration after flashing (especially when fresh nano used). Set Freq (eg. 182000), Set BFO (eg. 11056.5) and also Touch screen calibration, as touch will not work if not calibrated. To enter Setup menu press encoder button until Setup menu will appear (~10s).

NOTE 5: Firmware prepared to use with original ubitx v6 without hardware mods or with minimal hardware mods. My hardware mods includes: short of R3 2k2 resistor for my straight key CW operation (not really needed - read more in 09_sp7etd section), S-meter (LM386 circuit from: http://www.hamskey.com/2018/05/creating-simple-s-meter-sensor-for-ubitx.html with use of 10uF capacitor), RF gain and rotary encoder clicktop/detents removal (https://ubitx.net/2018/03/04/remove-detents-from-your-encoder/). You can read about them in this text or search the web, but these mods are not needed (not necessary) to use with this firmware.

See 11_sp7etd_screenshot.jpeg file for menu overview. 

Detailed instructions and revision history below.

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

04_sp7etd release notes (first major sp7etd firmware release for ubitx v6):

Introduction:

Hello, I have bought ubitx v6 some time ago and at beginning I was a little disappointed with CW performance and some functionalities. Decided to adjust it to my needs with default ILI9341 320x240 TFT display and then I have discovered beauty of this open project. I would like to take this opportunity to thank the creator of this project Ashhar Farhan VU2ESE, as well as all the people thanks to whom this wonderful project lives and becomes better. Today, when I am writing this text I am after couple weeks (mainly during my holidays) with this rig. During this time I was able to make a lot of QSO's. With ubitx v6 and with mini amplifier (based on IRF 530 mosfets, mini PA ~30-50W) I was participating IARU HF 2024 contest. From central Poland I made QSOs with Brasil, Argentina, Japan, USA, Puerto Rico, China, Oman and my first time with Hawaii. Still some HW mods are planned to be made based on data from ubitx websites (especially Hi-Per-Mite type CW audio filter).

These are some points summarizing my firmware mods:

a) jog tuning (digit tuning - usdx tuning style) implemented instead of dynamic tuning

By default jog position is set to 0.1 digit. Short press of the knob shifts jog position to the right (eg. to 0.01), pressing little longer shifts jog to the left (e.g. to 1, 10 and 100 respectively). Actual jog position is displayed at the bottom right corner of TFT screen (.01, .1, 1, 10 and 100). So, this firmware allows for 0.01 kHz step tuning while original firmware allows for 0.05 kHz minimal step.

b) Discovered that function checking TFT touch screen is sometimes causing audio noises (possible due to SPI). With this firmware You can toggle function for scanning TFT touch ON/OFF with ~5 seconds press and release of the knob. Status of touch sensing is indicated by "t" letter at the lower right corner of TFT screen (just after jog position indicator).

c) CW keying is modified. Discovered that start of CW TX is delayed and cutting out e.g. first dot in "R" letter (.-.) - first dot was not transmitted. Some mods were made and CW TX seems to be OK. now. Couple CW QSOs made with straight key.

d) Additionally discovered that CW TX frequency was shifted by sidetone +/- depending if USB or LSB was selected. This shift was commented out and CW TX occurs now on displayed/selected frequency (07_sp7etd: as later found in 04_sp7etd release still was issue with CW USB; since 07_sp7etd this is also fixed).

e) Some cosmetic and SW stability changes e.g. to display pop ups - some pop up messages where shifted to improve cosmetics. Some stability issues found (original firmware was not working stable with my usb-c type arduino nano). Seems to be OK. now.

Summarizing, button knob has 5 functions now (depends on pressing time):

Short press - jog position to the right.
Little longer press - jog position to the left (jog position is displayed on the right bottom corner).
Knob press up to 5s - do commands as in origin firmware - jump with cursor through the menu.
Knob press between ~5s and 10s - toggle TFT touch sensing ON/OFF - sometimes SPI noise can be heard - so toggling touch OFF can help in RX.
Long ~10s press until Setup window appear - as in origin firmware

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

07_sp7etd release notes:

a) RX shift when in CW mode and when in USB is fixed now. Whenever in LSB or in USB in CW mode - RX is now on the same frequency as TX.

b) "LCK" button added - lock of frequency tuning to disable encoder (to avoid accidental tuning).

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

08_sp7etd release notes:

a) S-meter and s-meter button added (s-meter button name is "0v8" - the number of sp7etd firmware release). I have used LM386 circuit from: http://www.hamskey.com/2018/05/creating-simple-s-meter-sensor-for-ubitx.html Schematic of s-meter circuit is included with this release (with use of 10uF capacitor). S-meter is turned OFF by default, because S-meter 300ms sampling may cause some noise on small signals. Turn s-meter ON by pressing "0v8". Mind s-meter indications are for reference only. S-meter scale: 1,2,3,4,5,7,9,10,20,30,40,50,60. "10" means 9+10dB etc. Due to hardware limitations of this solution - s-meter values slightly depends on volume level - especially at lower signals.

So, now last line shows: From the left: shortened CW status (wpm and tone frequency without units), s-meter indicator (grey color) if s-meter turned ON, two buttons: "0v8" as s-meter button, "LCK" as tuning LOCK button. On the right: jog position and TFT touch status - presence of letter "t" indicates touch sensing ON - absence OFF (eg. .1t, .01t etc.)

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

09_sp7etd release notes:

a) immediate change of USB/LSB mode after SSB mode select (no need to tune).

b) Some small optimization and simplification of sp7etd code. Example: use of "extern int" instead of "int export()" for some implemented earlier integers (still learning :). 



Best regards.

Tomasz sp7etd

Post scriptum:

Hardware mods:

RF Gain: I have installed RF GAIN. I have decided to install 10k potentiometer in series with R12 100ohm resistor and it is working great. Schematic of this implementation can be found with 08_sp7etd release files. Actually it should be little more than 10k (maybe 15k, 20k, 22k? - because 10k is not starting from "0" audibility), but for me it is enough to eliminate distortions from very strong stations.

CW Key: For straight key operation I have shorted R3 2k2 resistor - but mind - my key have tip and center ring shorted - I am using my key with other transceiver.
This R3 short is not needed if You are using stereo jack and key is shortening tip with sleeve only (while center ring is not connected).

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

10_sp7etd release notes (17th August 2025):

Current values of Frequency and BFO calibration are read from EEPROM and displayed on the screen in setup menu.

Mind - during start of ubitx - frequency and BFO calibrated values are read from EEPROM memory (init settings).
If these values are way off given range (e.g. values are not calibrated or wrong calibrated) - default values are set and written to EEPROM.
Allowed range for Frequency calibration:
from -2000000 to 2000000 (+/- 2 millions), default offset = 0 (in my two units ubitx v6 - frequency calibration are respectively 179375 and 192500).
Allowed range for BFO calibration:
from 11.048.000 to 11.060.000, default value 11.056.500 (changed default from 11.053.000).

To skip calibration - just turn OFF and power back ON.

Best regards

Tomasz sp7etd

PS. 10_sp7etd firmware - just quick, bench tests are done and OK. but mind no field - no on air tests performed yet.

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

11_sp7etd release notes (18th August 2025):

Automatic change of modulation LSB/USB after band selection (LSB: 80m & 40m, rest - USB).

Best regards

Tomasz sp7etd

PS. 11_sp7etd firmware - just quick, bench tests are done and OK. but mind no field - no on air tests performed yet.

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

SHORT INSTRUCTION - HOW TO FLASH UBITX V6:

Directly after downloading zip file (e.g. ubitxv6-11_sp7etd-ubitx_v6-11_sp7etd.zip) extract it and then rename extracted folder to the same as "ino" file (without ino extension).
So, Your "ubitxv6-11_sp7etd-ubitx_v6-11_sp7etd" directory rename to "ubitx_v6_11_sp7etd".
Then after starting Your Arduino IDE environment choose file -> open -> ubitx_v6_11_sp7etd.ino file.
All the files within directory should be opened. This is needed to proper flash Your arduino nano.
If files will not be in directory with proper name, after opening ubitx_v6_11_sp7etd.ino file - Arduino will ask You if it can create directory with this name.
In this case remember to move all unziped files to this directory (files will be opened by Arduino IDE).
Then disconnect 12V from Your ubitx. Connect USB cable between computer and arduino nano board (after that my screen of ubitx goes white).
In Arduino IDE select board (in the search box - write nano and select Arduino Nano), select Your port (my is /dev/ttyUSB0 Serial Port (USB) because its linux).
Mind, sometimes it happens that few plugs-unplugs are needed to show Your nano and USB port.
When Nano board is recognized font of it in drop down list will be BOLD.
Go to Sketch > Verify/Compile (or press "check" icon).
If program compiles without errors - You can Upload to Nano (Sketch -> Upload or "arrow to the right" icon).
Neglect any blurred screen after flash, just disconnect USB cable and power Your ubitx with 12V power (remember to use dummy load).
Perform calibration (press encoder for ~10s until Setup menu appears).
Any feedback welcome.

PS. Instruction written in Linux Arduino IDE, but - I believe - there are not too much differences to Win version.
