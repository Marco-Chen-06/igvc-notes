## Tentative Notes from Meetings/Discussions
These notes are for general architecture considerations for differents parts of the car. Once these decisions are validated, then I'll update them into the official notes such as [[Firmware]], [[Algorithms]], [[Hardware]], among others. If one of these tentative architecture considerations gets accounted for in the official notes, I will mark it with a checkmark (✓).

### Drive Node
- There should be 2 control loops
	- We want atomic updates (one-element FreeRTOS queue explained below)
	- One core handles communication 
		- Receives commands over CAN from the compute unit and drops the latest command into a one-element FreeRTOS queue (the control core can access this mailbox)
		- Reads IMU and also sends back things the compute unit needs (measured wheel speed, encoder counts, IMU data, heartbeat).
		- Most of these things are at irregular/unpredictable time intervals which is why communication needs its own core.
	- Another core handles feedback control
		- Every T (period) seconds, it reads the FreeRTOS command queue that the communication core may have updated, and reacts accordingly.
		- There is a timing requirement here which is why it feedback control has its own core.
- On the encoder interrupt topic
	- I looked more into it and rp2350 has a pio peripheral which suits this very well 
	- "Each PIO can independently execute sequential programs to manipulate GPIOs and transfer data" (RP2350 DS, 791)
	- PIO basically a tiny core designed to run simple state machines
	- [Ofifcial pico-examples quadrature encoder pio code](https://github.com/raspberrypi/pico-examples/blob/master/pio/quadrature_encoder/quadrature_encoder.c)
	- We can query the encoder count at any time without needing any interrupts in our control loops

## Misc
- We will use a 12-24V battery
	- One for motor controller, one for the compute?
	- Reasoning is that safety buton doing the hardware estop is separate from the compute units
- We will have one shared ubuntu machine to run our stack so that we don't run into dependency issues
- Lidar interfacing is a algorithms/ROS job
- We should have some sort of UI, maybe using Pyqt designer, so we don't have to flash in commands to test stuff

## Questions
- How many picos do we need?
- What is the input voltage of a pico for the rp2350?
- How do we flash the microcontroller without the breakout board? (Probably BOOTSEL or something)

