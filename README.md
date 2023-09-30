## Introduction
As a lifelong resident of the Bay Area, I have seen countless BART trains fly by, always giving off their signature high pitched howl as they barrel down the tracks. BART is a very unique urban transportation system, and although it is not the most efficient, I have grown to love riding it between the East Bay and San Francisco. 

The project outlined below is a fully custom model train, based off of the BART system. It was built to showcase skills in multiple facets of electrical engineering, as well as to be a homage to the legendary train.

A brief example of the train running can be seen [here](https://youtu.be/NTuRKBK8t7I)

## System Breakdown
At a high level, this project can be broken down into the following four major subsystems:

 1. Train Electronics
 2. Train Chassis
 3. Track Electronics
 4. Track Design

At the current time of writing, I am working on version 2 of the project, so the subsystem descriptions below will correspond to that version.

### Train Electronics
The train houses the entirety of the electronics it needs to operate autonomously. The main processing is all done on a Raspberry Pi 4B+, that is powered by a Geekworm X728 uninterruptable power supply (UPS) with two 18650 batteries. In order to know where it is located on the tracks, the Raspberry Pi is connected to an RC522 RFID sensor via SPI. The RFID tags are embedded in the tracks, and are manually preset to have "full speed", "slow", or "medium speed" values. After detecting these tags, the RFID sensor communicated back to the Raspberry Pi and the train enters the speed level corresponding to the tag.

In order to control the motor, the Raspberry Pi outputs logic signals to a custom PCB based around the L293D IC. The PCB has six logic inputs, external power input, two motor output terminals, and two status LEDs for debugging. The PCB is fully custom designed in KiCAD and was fabricated by PCBWay. The PCB can officially support up to 1A for each motor channel, but this number could possibly be higher in the future after some testing and possible integrating a cooling solution.

The train operates using a live third rail, which is currently running at 12V DC. Power from the third rail feeds in from two wires mounted on a side bracket (details on the mount can be found in the following section) and into the power delivery PCB and the Raspberry Pi UPS. The power is stepped down from the 12V to 5V with a simple DC-DC converter to match the needed input on the UPS. In the built configuration, the third rail is continually charging the battery cells on the UPS, which in turn power the Raspberry Pi. Since there are no metal tracks to ground the system, there is a hidden "fourth rail" running in the middle of the trackbed. An identical connection is made from the train to this rail in order to ground the system. 

The drivetrain of the train is based around a single DC motor that can be run in the 5-12V range. More about the drivetrain can be found in the *Train Chassis* section below.

### Train Chassis
The train chassis is entirely custom designed, using a mix of OnShape and TinkerCAD depending on the complexity of the parts. All elements of the chassis are 3d printed except for the ball bearings, which were purchased preassembled. The main chassis of the train is a flat plane with cutouts for the gears (more on those later). The top of the chassis features a slide mount for the Raspberry Pi and a vertical mounting bracket for the power delivery PCB, as well as a mount for the DC motor. In order to transfer power from the live third rail, there is a side mounted bracket to guide wires down from the Raspberry Pi and power delivery PCB. An identical mount runs through the gear cutout on the chassis to provide the ground line connections. The bottom of the chassis is reinforced with 3 extra strips of PLA running along the length of the train, while also featuring mounts for the bearings. The two axles are 1/4" diameter and have wheels friction fit on either end. The train wheels are conical in shape, with an exaggerated flange for extra stability on the small scale.

The drivetrain of the system consists of a DC motor with a 10 tooth gear and a 15 tooth gear mounted on the rear axle. A pulley is used to transfer power between the gears. The current gear ratio is still being iterated on, to find the right performance level for the scale.

### Track Electronics
The trackbed electronics are very simple in theory, but are currently difficult to maintain. The live third rail and grounding fourth rail are both 3d printed from PLA, with a layer of conductive copper tape stuck to the top of each. This copper tape preforms good enough for my needs, with about 5 ohms of resistance measured over 20 inches of rail. The downside of using the copper tape to add conductivity to the rails is its general structural weakness. The tape tears very easily, and wears out over time with the wires from the train car rubbing against it. Adding more tape on top of the worn tape can fix these problems, but also sometimes results in a loss of conductivity along the rail.

In order for the train to control itself, RFID tags are laid within the trackbed, between sleeper planks. Standard 13.56MHz RFID tags are used, in order to keep the system lower cost and less complex.

Power is provided to the third rail and grounding rail at one end of the trackbed, with a standard bench power supply.

### Track Design
The trackbed is a simple 3 rail design, with a small fourth rail running down the center of the tracks. The main rails are spaced with 3.375" between the center of each rail, with the third rail being 1.125" to the right of the trackbed. Each rail segment is 5" in length, and is supported by a sleeper plank at each end. The overall track dimensions were built out after the train chassis was assembled, to ease the design constraints on that part of the project.


## Current Features
The train currently can operate autonomously on a straight section of track, with the third rail running at 12V. A command is issued to the train to start moving initially, and then the Raspberry Pi takes over and controls the train's speed by reading RFID tags, as mentioned above. The train can slow down, speed up, and come to a complete stop autonomously. 

## Future Work
As of September 2023, I am working on optimizing the drivetrain of the system so it runs smoother along the rails. I am currently experimenting with ways of adding grip to the tracks, as well as with ways to better contact the third rail for more consistent power delivery. After these two parts of the system are finished, I will begin experimenting with the train's turn radius to find a suitable dimension to build curved sections of track. I anticipate this will be a longer process, and plan on building out a longer section of straight track simultaneously, to optimize the train control system and find the speed limits of the system. 

### End Notes
I will also be updating this GitHub repo with 3d models, code, images, and more over the coming weeks, so check back periodically if you are interested in the project. 

**I am also looking for work in the electrical engineering field, feel free to reach out if you have any leads.**