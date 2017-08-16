<link href="style.css" type="text/css" rel="stylesheet"></link>

# cell
Python 2.7 code to interface a cheap 2G SIM800L to a cheap Raspberry Pi Zero W v1.1

| <a href="https://www.ebay.com/sch/i.html?_nkw=sim800+gprs+gsm+module+board+l+shape"><img src="https://github.com/lizard43/cell/blob/master/images/SIM800L.jpg" width="200" /></a> | <a href="http://microcenter.com/product/475267/Zero_W"><img src="https://github.com/lizard43/cell/blob/master/images/raspberry-pizero.png" width="200" /></a> |
|-|-|

## License
- MIT

## Parts

- Get a Raspberry Pi Zero W at [Micro Center](http://microcenter.com/product/475267/Zero_W) for $10 in-store pickup.

- Get a SIM800L on [eBay](https://www.ebay.com/sch/i.html?_nkw=sim800+gprs+gsm+module+board+l+shape) for about $10 w/ free shipping:

- Get a free 1M/month SIM card from [hologram](https://hologram.io/devplan)

## OS

- Using Raspbian Jessie version 2017-0705 found at [Raspberry Pi Downloads](https://www.raspberrypi.org/downloads/raspbian)

- After flashing the Raspbian to an SD card
	- Edit the /boot/command.txt and /boot/cmdline.txt files to enable the UART on the Pi Zero's GP14 (TX) and GP15 (RX)
	- Look at my files here in the repo to see the edits I made

## Activate
- If you're using the free hologram.io SIM card (and if not, why not?), [activate](https://dashboard.hologram.io/activate) the SIM and choose the Developer Data Plan

## Connections

- Hook up the SIM800 to the Pi Zero with a few wires:

| <img src="https://github.com/lizard43/cell/blob/master/images/SIM800L.sides.jpg" width="450" /> |  <img src="https://github.com/lizard43/cell/blob/master/images/Raspberry-Pi-GPIO.2.png" width="800" />  |
|-|-|


- Insert your SIM card into the SIM800

## Check It Out

- Install picocom to test connectivity
	sudo apt-get install picocom

- Start picocom
	picocom --baud 9600 /dev/ttyAMA0

- See if SIM800 is alive with the 'AT' command. The SIM800 should respond with 'OK'

- Read the SIM800 reference files in the repo's doc folder for many commands

## Running with the Python Code

- The version of Raspbian I used comes with Python 2.7.9 so that's the version I have targeted with this code.

- I don't 'know' Python so I learned some as I cobbled this code together. It ain't pretty and I stole lots from others. But it ~works for my purposes and it's free

- Install psSerial (this installed v3.4 for me)
	- sudo pip install pySerial

	- pySerial has [decent docs](http://pyserial.readthedocs.io/en/latest/shortintro.html)

- Install Pmw (this installed v2.01)
	- sudo pip install Pmw

	- Pmw is a toolkit for building a UI in Python using the Tkinter module. You can find docs at the [Pmw Site](http://pmw.sourceforge.net/docs)
		- But the more recent v2 docs seem to be only provided in the tar.gz that you can download [here(https://sourceforge.net/projects/pmw/files/Pmw2)

- Run the cobbled code:
	- python cellComms.py

- Open the serial port with the Open button

- Send an 'AT' command with the AT button

- Get the SIM card IMEI with the IMEI button
	- This sends an 'AT+GSN'

- Get the SIM800 module version with the SIM800 button
	- This sends an 'AT+CGMR'

- Get the signal strength in bars with Bars button
	- This sends an 'AT+CSQ'

- Set the APN with the APN button
	- This button sends an 'AT+CSST=hologram'
		- I've hard coded my APN to hologram since that's the SIM card I'm using
		- Edit the APN constant in the code to change to whatever you're using

- Get the Network status with the Net button
	- This sends an 'AT+CREG'

