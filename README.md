## Introduction
As a lifelong resident of the Bay Area, I have seen countless BART trains fly by, always giving off their signature high pitched howl as they barrel down the tracks. BART is a very unique urban transportation system, and although it is not the most efficient, I have grown to love riding it between the East Bay and San Francisco. 

The project outlined below is a fully custom model train, based off of the BART system. It was built to showcase skills in multiple facets of electrical engineering, as well as to be a homage to the legendary train.

## System Breakdown
At a high level, this project can be broken down into the following four major subsystems:

 1. Train Electronics
 2. Train Chassis
 3. Track Electronics
 4. Track Design

At the current time of writing, I am working on version 2 of the project, so the subsystem descriptions below will correspond to that version.

### Train Electronics
The train houses the entirety of the electronics it needs to operate autonomously. The main processing is all done on a Raspberry Pi 4B+, that is powered via an uninterruptable power supply (UPS) with two 18650 batteries. In order to know where it is located on the tracks, the Raspberry Pi is connected to an RC522 RFID sensor via SPI. The RFID tags are embedded in the tracks, and are manually preset to have "full speed", "slow", or "medium speed" values. After detecting these tags, the RFID sensor communicated back to the Raspberry Pi and the train enters the speed level corresponding to the tag.

In order to control the motor, the Raspberry Pi outputs logic signals to a custom PCB based around the L293D IC. The PCB has six logic inputs, external power input, two motor output terminals, and two status LEDs for debugging. The PCB is fully custom designed in KiCAD and was fabricated by PCBWay. The PCB can officially support up to 1A for each motor channel, but this number could possibly be higher in the future after some testing and possible integrating a cooling solution.

The drivetrain of the train is based around a single DC motor that can be run in the 5-12V range. More about the drivetrain can be found in the *Train Chassis* section below.
### Train Chassis

### Track Electronics

### Track Design


## Coming Soon! Last updated 9-27-23