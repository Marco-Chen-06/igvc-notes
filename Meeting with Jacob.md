
## Important Questions
- What did algorithms do when no firmware or hardware was built?
	- What's the earliest useful thing that algorithms could start testing on? (Simulation?)

Agos is perception vs sensing stack

given cost map, how do you navigate the course
but constructing costmap isnt trivial

selfdrive repo
hardware and firmware are in the main branch
All algos stuff is in user branches

they just did evertthing in the car at the same time but there is aslso a smaller car

- The IGVC report mentions ROStouCAN to interface between CAN nodes and ROS nodes. Can you walk us through the method of how this system worked, including how algorithms gets sensor data? (Also what is ROStouCAN?) (Line 71)





- How confirmed was your frame/chassis before firmware or electronics started? Moreso, did you build the frame around the electronics or the electronics around the frame?
- How much of the mechanical work required dynamics/mechanical depth? Do you recommend we handle the mechanics ourselves, or should we consider recruiting MechEs?
- Who owns the github Autonomy Lab organization and how do we get back in? https://github.com/autonomy-lab-cooper-union
## Less Important Questions
- At the competition, if anything, what surprised your team the most that the rulebook did not prepare any of you for?
	- the competition it not the best adminsitraitno i love igvc administration
- Looking back, what did you sink way more time into it than it turned out to deserve, and what did you unverinvest in that turned out to matter a lot more than you expected?


FIRMWARE DELEGATION
- everyone wrietes their own drivers independehtly.
- then we do all theintegration into freertos
- but we try to minmize the assumptions so its not hell to integrate
- so everyone is building independently and then when we have a solid foundation then we stuff everything together


## Meeting Notes

### Firmware Delegation (Suggestion)
- Everyone writes their own drivers independently
- Deal with the freertos and code integration later
- Preferably we 