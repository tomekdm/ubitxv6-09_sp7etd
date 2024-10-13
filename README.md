"08_sp7etd firmware update manual"

GENERAL NOTES:

NOTE 1: Firmware originated from v6.3.1 Arduino sketch. For use with original ILI9341 320x240 TFT display.

NOTE 2: Mind to rename unpacked directory eg. "ubitxv6-08_sp7etd-master" to the same name as *.ino file (eg. "ubitx_v6_1_code_08_sp7etd").

NOTE 3: Remember to perform FULL calibration after flashing (especially when new nano used). Set Freq (eg. 182000), Set BFO (eg. 11056.5) and also perform Touch screen calibration, as touch will not work if not calibrated. To enter Setup menu press encoder button until Setup menu will appear (~10s).

NOTE 4: After switching from LSB to USB - and vice versa - remember to perform a tune. Even small frequency step is required to switch transceiver into selected modulation (09_sp7etd firmware is already prepared with fix for this issue - immediate USB/LSB mode change - ready for download in release section, but mind it is not tested in the air yet - bench tests shows correct operation of 09_sp7etd firmware).

NOTE 5: Firmware prepared to use with original ubitx v6 with no hardware mods or minimal hardware mods. My hardware mods includes: short of R3 2k2 resistor for CW straight key operation, S-meter and RF gain. You can read about them in this text, but these mods are not needed to use with this firmware.
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

04_sp7etd release notes (first major sp7etd firmware release for ubitx v6):

Introduction:

Hello, I have bought ubitx v6 some time ago and at beginning I was a little disappointed with CW performance and some functionalities. Decided to adjust it to my needs with default ILI9341 320x240 TFT display and then I have discovered beauty of this open project.
I would like to take this opportunity to thank the creator of this project Ashhar Farhan VU2ESE, as well as all the people thanks to whom this wonderful project lives and becomes better.
Today, when I am writing this text I am after couple weeks (mainly during my holidays) with this rig. During this time I was able to make a lot of QSO's.
With ubitx v6 and with mini amplifier (based on IRF 530 mosfets, mini PA ~30-50W) I was participating IARU HF 2024 contest.
From central Poland I made QSOs with Brasil, Argentina, Japan, USA, Puerto Rico, China, Oman and my first time with Hawaii.
Still some HW mods are planned to be made based on data from ubitx websites (especially Hi-Per-Mite type CW audio filter).

These are some points summarizing my firmware mods:

1. jog tuning (digit tuning - usdx tuning style) implemented instead of dynamic tuning

By default jog position is set to 0.1 digit. Short press of the knob shifts jog position to the right (eg. to 0.01), pressing little longer shifts jog to the left (e.g. to 1, 10 and 100 respectively). Actual jog position is displayed at the bottom right corner of TFT screen (.01, .1, 1, 10 and 100). So, this firmware allows for 0.01 kHz step tuning while original firmware allows for 0.05 kHz minimal step.

2.  Discovered that function checking TFT touch screen is sometimes causing audio noises (possible due to SPI). With this firmware You can toggle function for scanning TFT touch ON/OFF with ~5 seconds press and release of the knob. Status of touch sensing is indicated by "t" letter at the lower right corner of TFT screen (just after jog position indicator).

3.  CW keying is modified. Discovered that start of CW TX is delayed and cutting out e.g. first dot in "R" letter (.-.) - first dot was not transmitted. Some mods were made and CW TX seems to be OK. now. Couple CW QSOs made with straight key.

4.  Additionally discovered that CW TX frequency was shifted by sidetone +/- depending if USB or LSB was selected. This shift was commented out and CW TX occurs now on displayed/selected frequency (07_sp7etd: as later found in 04_sp7etd release still was issue with CW USB; since 07_sp7etd this is also fixed).

5.  Some cosmetic and SW stability changes e.g. to display pop ups - some pop up messages where shifted to improve cosmetics. Some stability issues found (original firmware was not working stable with my usb-c type arduino nano). Seems to be OK. now.

Summarizing, button knob has 5 functions now (depends on pressing time):

1) Short press - jog position to the right.
2) Little longer press - jog position to the left (jog position is displayed on the right bottom corner).
3) Knob press up to 5s - do commands as in origin firmware - jump with cursor through the menu.
4) Knob press between ~5s and 10s - toggle TFT touch sensing ON/OFF - sometimes SPI noise can be heard - so toggling touch OFF can help in RX.
5) Long ~10s press until Setup window appear - as in origin firmware

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

07_sp7etd release notes:

Release NOTE 1: 

RX shift when in CW mode and when in USB is fixed now. Whenever in LSB or in USB in CW mode - RX is now on the same frequency as TX.

Release NOTE 2: 

"LCK" button added - lock of frequency tuning to disable encoder (to avoid accidental tuning).

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

08_sp7etd release notes:

Release NOTE 1: 

S-meter and s-meter button added (s-meter button name is "0v8" - the number of sp7etd firmware release). 
I have used LM386 circuit from:
http://www.hamskey.com/2018/05/creating-simple-s-meter-sensor-for-ubitx.html
Schematic of s-meter circuit is included with this release (with use of 10uF capacitor). S-meter is turned OFF by default, because S-meter 300ms sampling may cause some noise on small signals. Turn s-meter ON by pressing "0v8". Mind s-meter indications are for reference only. S-meter scale: 1,2,3,4,5,7,9,10,20,30,40,50,60. "10" means 9+10dB etc. Due to hardware limitations of this solution - s-meter values slightly depends on volume level - especially at lower signals.

So, now last line shows: 
From the left: shortened CW status (wpm and tone frequency without units), s-meter indicator (grey color) if s-meter turned ON, two buttons: "0v8" as s-meter button, "LCK" as tuning LOCK button. On the right: jog position and TFT touch status - presence of letter "t" indicates touch sensing ON - absence OFF (eg. .1t, .01t etc.)

See 08_sp7etd_screenshot.jpeg file for menu overview.

Best regards.

Tomasz 
sp7etd

Post scriptum:

Hardware mods:
1. RF Gain:
   Last time I have installed RF GAIN. I have decided to install 10k potentiometer in series with R12 100ohm resistor and it is working great. Schematic of this implementation can be found with 08_sp7etd release files. Actually it should be little more than 10k (maybe 15k, 20k, 22k? - because 10k is not starting from "0" audibility), but for me it is enough to eliminate distortions from very strong stations.

3. CW Key
   For straight key operation I have shorted R3 2k2 resistor (I am not using paddle).
