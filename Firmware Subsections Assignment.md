Hi everyone. Really great work on the debugging setup and getting the LEDs to blink. Big assignment this week (should be easier than last week tho)

The goal for autonomy lab this year is that everyone gets experience working on challenging projects outside of coursework. And in the end, we send off a working car where every member has worked deeply on a specific subsystem, into the IGVC AutoNav competition. 

So for this week, you will all get to choose a firmware subsection (subsection options listed in bottom half of this post) of the car that you will take authority over for this year. Max 2 people per section. You will make the decisions for your subsection, such as how the code works, what sensor/part to use, and how it connects to the rest of the car. You will be expected to understand your subsection better than anyone else on the team, including me.

We also skinned alive the Cooper Union Autonomy Lab Autonomous Scooter for parts. We found 2 MD30C R2 30A DC Motor Drivers, 2 motors and probably some encoders. (Not sure of the model of motors and encoders yet, will update if I find out)

## Deliverable (Sunday 10/11 and Friday 10/16 Deadlines)
- Pick the section and comment it under this post (Comment by Sunday 10/11). I'll add you if you already told me in person, too. 
- By Friday 10/16, make a slide presentation (or whatever format you want) and present it for about 5 minutes to all firmware members. They can literally be the crappiest slides ever and you can read off notes. The point is to show you've read the rules and done research and are ready to lead your section.
- Cover the following in your slides: (mandatory)
	- What is your section, and why do we need it? (1-2 sentences)
	- What do the IGVC 2026 rules (2027 rules haven't come out yet) say about it? Include quotes. If the rules don't mention it directly, which rules does it help us meet?
	- What parts will you need? If applicable, consider leftover parts from the Autonomous Scooter (Choose whether to keep or replace parts, and why). If you want to buy something, include the part, link, price, and why this part specifically. 
	- Questions you have. Things you are unsure of, what might you need help from hardware or algorithms or us?
- If you have extra time (optional, not required)
	- What did Cooper Union SelfDrive or an IGVC 2026 AutoNav team do for this subsection?
	- When the picos arrive, what do you plan to work on first?
- Things to consider when picking a part we will buy:
	- Our team's budget is only $500 rn, we might get more. So aim for $30-60 per sensor. 
	- Outdoors, mechanical vibrations, rain, big motors nearby (causing EMI)
	- Sensor is well documented/popular enough that you can write a driver for it
	- Pico's GPIO pins operate with 3.3V logic and ADC pins measure 3.3V max. Any voltage can power your part (we'll have a power distribution board) but if your sensor's data lines are like 5V or 12V things might get harder. 

## Resources
- 2026 IGVC rules: http://www.igvc.org/2026rules.pdf
- IGVC 2026 design reports: http://www.igvc.org/d2026.htm
	- The best ones in my opinion:
	- Lawrence Technological University - Turbo Blue 2.0 (They run 3 RP2040 Picos communicating over CAN): http://www.igvc.org/design/2026/19.pdf
	- Indian Institute of Technology Madras (They documented their electronics and safety requirements well. Note their report is for both SelfDrive and AutoNav): http://www.igvc.org/design/2026/9.pdf 
- Cooper Union SelfDrive Monorepo: https://github.com/CooperUnion/selfdrive
- Autonomy Lab Autonomous Scooter Main Repo: https://github.com/autonomy-lab-cooper-union/autonomous-scooter
- Autonomy Lab Autonomous Scooter Code: https://github.com/autonomy-lab-cooper-union/autonomous-scooter-arduino

## Car Architecture
Here are notes I have for our car's planned architecture. Everything is subject to change, especially since you guys will learn a lot about your sections. It's likely I missed many things too.
- Two Raspberry Pi Pico (RP2350) boards/nodes, each running FreeRTOS.
	- Drive node: Controls motor drivers, wheel encoders, IMU, speed control
	- Safety/body node: Reads mechanical e-stop, wireless e-stop, start button, battery voltage, and mode switch. Controls safety light and CAN heartbeat.
	- The two nodes communicate over CAN, using our CAN controller boards created last semester. The algorithms computer listens to the same CAN bus using a USB-CAN adapter and gets the data through ROS. 
	- Still undecided if we are doing differential drive or steering. This mainly affects motors and encoders.

## Firmware Subsections
### IMU (Members: Andrew Chu + 1 Open Slot)
- Measures how the car accelerates and turns. Algorithms will make good use of accelerometer and gyroscope data.
- I think we have 2 IMUs coming in next week already.
### Wheel Encoders (Members: 2 Open Slots)
- Measures how far and fast each wheel turns. Used for tracking the car's position and for speed control.
- We have 2 encoders on the scooter (I'll confirm the model tomorrow)
- Look into RP2350's PIO peripheral for reading them. Official quadrature encoder example: https://github.com/raspberrypi/pico-examples/tree/master/pio/quadrature_encoder
### Safety/Body (Members: 2 Open Slots)
- Safety light, wireless & mechanical e-stop, mode switch, start button, battery voltage, CAN heartbeat
- The car cannot qualify at all without this subsection, and the rules are pretty specific.
- We have an e-stop button on the big car in 701, not sure if it still works.
### Motors (Members: 2 Open Slots)
- Drives motors and makes the wheels go the speed the algorithms team wants it to go.
- We have 2 motor drivers from the scooter (Cytron MD30C). The 2026 IGVC IIT team used this driver too. The scooter has motors too (I'll confirm the model tomorrow). 
- We aren't sure if we are doing differential drive or steering yet
### CAN (Members: Marco Chen + 1 Open Slot)
- The communication protocol that lets the two picos and the algorithms computer talk to each other.
- We have our MCP2518FD CAN driver and boards from last semester.

Note: The Velodyne lidar connects to the algorithms computer over Ethernet and is read through ROS, so it's 98% an algorithms job. If you are really interested in working on the lidar, you can tell me. You can still choose a firmware section too, if you want.

Also: Picos have been ordered, not certain when they will arrive though. I will provide updates on this. 

Let me know if you have any questions or concerns. 