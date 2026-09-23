The firmware will be split up into two microcontroller nodes, each running FreeRTOS. One drive node, and one safety/body node.

The two microcontroller nodes will communicate with eachother through CAN.

## Drive Node
This node will manage both motor drivers, both motor encoders, and the IMU. 

## Safety/body Node
This node will manage the wireless e-stop, mechanical e-stop, mode switch (between manual and autonomous mode), 'start' button, safety light, power monitoring, CAN heartbeat (IIT did this). 

## How Algorithms Will Get Data
Each MCU will spit out queued data and put it on the CAN bus. Then the algorithm just plugs the innomaker into their computer and does their ros or python or stuff.