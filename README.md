Initial project by Vladimir Komendantskiy

Uploaded to GitHub for backup purposes by Benoit-Pierre DEMAINE.

With greatings to ForKicks
http://www.orangepi.org/orangepibbsen/forum.php?mod=viewthread&tid=4208&pid=45047&page=1&extra=#pid45047

Tested to work by Benoit-Pierre Demaine with
- SH1106 OLED 128x64 screen
- Orange Pi Zero
- Armbian_5.35_Orangepizero_Ubuntu_xenial_next_4.13.16

As this git tree is intended to only be a backup, live version will be stored at
https://github.com/doublehp/ssd1306-i2c-opiz_Demaine

The following tutorial is copied from 
http://www.orangepi.org/orangepibbsen/forum.php?mod=viewthread&tid=4208&pid=45047&page=1&extra=#pid45047

###############################################################

Orange Pi 0.96 inch OLED Module 128x64

ForKicks

Post time 2019-3-1 06:31:49

Just wanted to make a quick note on geting started with the i2c oled display.This procedure should be very similar on a different board running armbian aswell.

1. In commandline: sudo armbian-config
2. In GUI: System -> Hardware -> Toggle on i2c-0 | Save, and follow instructions
3. In commandline: sudo apt-get update -> sudo apt-get install i2c-tools
4. In console: i2cdetect -r 0

You will be greeted with this(Awnser yes):

WARNING! This program can confuse your I2C bus, cause data loss and worse!
I will probe file /dev/i2c-0 using read byte commands.
I will probe address range 0x03-0x77.
Continue? [Y/n] Y
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- 3c -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --


0x3c is the address of the display (not 0x78 as shown on ali).
If you did not get 3c, you will need to make a note of the result.
Second note, if there are more than one device, there will be more than one result.

There is no point in contiueing with the next points until you get a positiv awnser from this test. If all the fields are blank eg. --, it means that there are no devices on the i2c-0 bus.
Possilbe error: Bad wiring, check it. Wrong i2c bus, might be an idea to test i2c-1 in the i2cdetect test. Bad device, or port, run the test on a nother board, possibly test it on Arduino.

5. Download and extract : https://drive.google.com/file/d/1jq2ddW927Cy1V0jbryz6P1cVFe428mIr/view?usp=sharing
6. Navigate in to the folder you just extrated. (If you did not get 3c in the i2vdetect test, you will need to edit the oled.h file. On line 16 you will find: #define OLED_I2C_ADDR      0x3c <--- change 3c to your result. Save and exit)
7. In console: make
8. In console: ./oled_demo

Congrats, you should now see demo information printed on your oled display and ready to make it show something more intresting than fake data

Hope I helped.

###############################################################
