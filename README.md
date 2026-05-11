# RocketVirus V0 Design Document
RocketVirus V0 is supposed to be a multi-purpose development and flight board built around the Heltec Wi-Fi Lora V3 for the use of rocketry. 
-	GNC Computer
-	LoRa Telemetry Link
-	Meshtastic Node
-	EX Engine Controller
-	Data Recorder
# SPI Periferals
The SPI busses are meant to be used for High Bandwidth Periferals including memory. The ESP32-S3 actually has 2 accessible SPI controllers, SPI2 and SPI3, (SPI0/1 is reserved for controller memory). The two controllers are not made equal.
SPI2 controller, is meant primarily for the management of flash memory and has additional features as a master. On the heltec, by default this serial controller drives the LoRa radio module, and the default FSPI pins are not broken out. The other Priority 1 FSPI pins are also used for other on board functions like LED write, Vext Control and ADC Control. On an integrated board it would be used to drive flash memory but as we do not have that luxury, we will leave this SPI driver alone to run the radio.
SPI3 controller will be the controller broken out to the user. It will drive a 32 MB NOR flash memory which will be used to safely record flight and experimental data. A micro SD card will be used for bulk storage and data transfer. Two more auxiliary SPI devices will be wired out via 7 pin JST GH connector as per the pixiehawk standard. 
-	MISO – GPIO 4
-	MOSI – GPIO 2
-	CLK – GPIO 38
-	FLASH CS – GPIO 33
-	SD CS – GPIO 34
-	AUX 1 CS – GPIO 39
-	AUX 2 CS – GPIO 40

# I2C Peripherals
I2C is meant to be primarily for the use of low bandwidth peripherals. Currently there will be no on-board sensors of this type, but I2C will be broken out to 4 pin JST SH using the stemma qt pinout.
-	SDA – GPIO 48
-	SCL – GPIO 47
Control Lines
The control lines amplify a control signal using external power in order to drive various electronics such as lights, buzzers, servos, ESCs, solenoids, and even pyrotechnics. From either 5V 
[Gate Circuit Design WIP]
[Protection circuits WIP]
[Power Connectors WIP]
-	Control 1 – GPIO 5
-	Control 2 – GPIO 26
-	Control 3 – GPIO 41
-	Control 4 – GPIO 42
# ADC Devices
Analog to digital converters allow for the device to measure analog signals like battery voltage, piezoelectric sensors, or even microphones.
[Calibration]
[Connector]
-	ADC 1 – GPIO 7
-	ADC 2 – GPIO 6
# Radio Communication
As previously mentioned when discussing SPI Periferals Heltec Wi-Fi Lora V3 is equipped with an SX1262 which works with both 433 MHz amateur radio band and 900 MHz. While we will primarily use LoRA in hopes of receiving live telemetry from the rocket, for faster transmission FSK can be used instead.
