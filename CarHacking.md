## Summary:
This is a guide to recreate an CAN attack to a emulated interfaz, to a car with and OBD and another attack for open the doors of a car.

## Description
In this case, need a kali linux virtual machine or preferably not virtual,a OBD wire, and a HackeRF. For the two first attacks needs can-utils, ICSim, and CANalyzat0r in kali and for the other attack need gnuradio,gspectrum analyzer in a pc (can be the same kali).
## Steps To Reproduce:
1. Install Can-utils
	1. Open a terminal and write
		- $ apt-get install can-utils
2. Setup a virtual CAN (no physical CAN port available).
	1. Install Virtual CAN module
		- $ modprobe vcan
	2. Verify Virtual CAN module is installed
		- $ modprobe -c | grep vcan
	3. Create a new network interface and Turn it on
		- $ ip link add dev vcan0 type vcan
		- $ ip link set up vcan0
3. Install Instrument Cluster Simulator
	1. Install ICSim dependencies
		- $ sudo apt-get install libsdl2-dev libsdl2-image-dev
	2. clone ICSim repository and go to the directory
		- $ git clone https://github.com/zombieCraig/ICSim.git
		- $ cd ICSim
	3. Start the simulator
		- $ make 
		- $ ./icsim vcan0
	4. Start the controls on a different terminal
		- $ ./controls vcan0
			- Can be accelerated up and down arrows and with left and right arrows can control the directional and with left/right shift unblock and block the car.
4. Analyse CAN data using CANalyzat0r
	1. Install Docker
		1. Add Docker pgp key:
			- $ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
		2. Configure Docker apt repository:
			- $ echo 'deb https://download.docker.com/linux/debian stretch stable' > /etc/apt/sources.list.d/docker.list
		3. Install Docker
			- $ apt-get install docker-ce
		4. Verify if it was installed correctly
			- $ docker run hello-world
	2. Clone CANalyzat0r and go to docker folder
		- $ git clone https://github.com/schutzwerk/CANalyzat0r
		- $ cd CANalyzat0r/docker
	3. Run make build and make run
		- $ make build & make run
	4. When CANalyzat0r open go to Manager tab and create a new project.
	5. Go to Main tab and select it as a active project
	6. Start the simulator and the control again.
	7. Go to Filter Tab in CANalyzat0r and change "0s" to "10"
	8. Click start and then in the new window that appears click it accept and in the controls start to accelerate or something else to send package for at least one minute.
		- Eg. [https://youtu.be/ztRUP436zds](https://youtu.be/ztRUP436zds)
	9. Accept again the new window that appears and wait for the analyze.
	10. When it finish select the package that you need and send it to the repeater tab.
	11. There click on Send all and see the simulator and you will see that it moves itself.
		- Eg. [https://youtu.be/9ZdabgO4g3c](https://youtu.be/9ZdabgO4g3c)
5. Repeat the previous steps but this time instead de CAN interface use the interface that is connected to the OBD wire.
6. Open a Car
	1. Connect the HackerRF to a laptop
	2. Install gnuradio-companion on it.
	3. Install gspectrum analyzer on it.
	4. Analyce the frequency of the key car
		1. Search in a page of keys the frequency of it
		2. Open gspectrum and put the frequency and the HackerRF device and run it.
			1. When the key is clicked it will send a pulse and it will be see in the analyzer
				- Eg. [https://youtu.be/6sJOphH8P10](https://youtu.be/6sJOphH8P10)
		3. Once analyzed, open GnuRadio
			1. Put the same values that put in the analyzer
			2. Click Run and click the key and then save it.
				- Eg. [https://youtu.be/1_eZA30l3p8](https://youtu.be/1_eZA30l3p8)
			3. Send it to a signal sink.
			4. Copy the signal information.
			5. And resend it to open the car.
				- Eg [https://youtu.be/pfxAmDbcEU8](https://youtu.be/pfxAmDbcEU8)
##Supporting Material/References:
[VirtualBox](https://download.virtualbox.org/virtualbox/6.0.6/VirtualBox-6.0.6-130049-Win.exe)

[Kali](https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/)

[Can-utils](https://github.com/linux-can/can-utils)

[ICSIM](https://github.com/zombieCraig/ICSim)

[CANanalyzat0r](https://github.com/schutzwerk/CANalyzat0r)

[GNURadio](https://www.gnuradio.org/)

[gspectrum](https://github.com/xmikos/qspectrumanalyzer)