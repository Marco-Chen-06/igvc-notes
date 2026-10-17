The firmware will be split up into two microcontroller nodes, each running FreeRTOS. One drive node, and one safety/body node.

The two microcontroller nodes will communicate with eachother through CAN.

## Drive Node
This node will manage both motor drivers, both motor encoders, and the IMU.  
- There are 2 control loops (possibly) (might have to think about atomic updates)
- One core does communication
- One does the feedback control loop for the motors

## Safety/body Node
This node will manage the wireless e-stop, mechanical e-stop, mode switch (between manual and autonomous mode), 'start' button, safety light, power monitoring, CAN heartbeat (IIT did this). 

## How Algorithms Will Get Data
Each MCU will spit out queued data and put it on the CAN bus. Then the algorithm just plugs the innomaker into their computer and does their ros or python or stuff.


## Encoders vs Interrupts
I looked more into it and rp2350 has a pio peripheral which suits this very well 

"Each PIO can independently execute sequential programs to manipulate GPIOs and transfer data" (RP2350 DS, 791)

 PIO basically a tiny core designed to run simple state machines

 [Ofifcial pico-examples quadrature encoder pio code](https://github.com/raspberrypi/pico-examples/blob/master/pio/quadrature_encoder/quadrature_encoder.c)

 We can query the encoder count at any time without needing any interrupts in our control loops