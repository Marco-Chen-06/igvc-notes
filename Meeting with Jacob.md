
## Important Questions
- What did algorithms do when no firmware or hardware was built?
	- What's the earliest useful thing that algorithms could start testing on? (Simulation?)
- The IGVC report mentions ROStouCAN to interface between CAN nodes and ROS nodes. Can you walk us through the method of how this system worked, including how algorithms gets sensor data? (Also what is ROStouCAN?) (Line 71)
- How confirmed was your frame/chassis before firmware or electronics started? Moreso, did you build the frame around the electronics or the electronics around the frame?
- How much of the mechanical work required dynamics/mechanical depth? Do you recommend we handle the mechanics ourselves, or should we consider recruiting MechEs?
- Who owns the github Autonomy Lab organization and how do we get back in? https://github.com/autonomy-lab-cooper-union
## Less Important Questions
- At the competition, if anything, what surprised your team the most that the rulebook did not prepare any of you for?
	- the competition it not the best adminsitraitno i love igvc administration
- Looking back, what did you sink way more time into it than it turned out to deserve, and what did you unverinvest in that turned out to matter a lot more than you expected?

## Meeting Notes
 Don't plug the RJ45 ports on the Gem into your computer because your computer will get destroyed

### Tooling, Environment, Build System
- Before, the Autonomy lab used docker.
- Jacob doesn't like docker because Docker forces you to use only the tools inside the docker container.
- Jacob recommends Nix because it overlays your environment instead of replacing it.
- Another option is like, for every subteam, we just document what packages we should install or what is necessary. So then we wouldn't really need Nix, but we really can't know unless we start working.
- Since LLMs exist, build system onboarding is not as complex as it used to be. You don't have to learn a new language anymore.

### ROS/Algorithms
- Jacob doesn't like ROS because it's a tumor that spreads into everything
- We still probably need it though. He recommends we write independent modules with defined input output format.
- Try to keep everything isolated from ROS

### Costmap (Algorithms)
- Algorithms is split into perception stack vs sensing stack
- The question is, given the costmap, how do we navigate the course?
- Note that creating the costmap itself is not trivial at all

### Zihan Question on Gazebo Being Slow
- X forwarding tries to re-render the window on your system and it's very heavy
- Instead, remote desktop software might be a better option

### Testing
- The entire selfdrive car was built at the same time, so they could already begin algorithm testing
- They did have Carrie which was a smaller car that they used to test on a smaller scale

### Selfdrive Repo
- Hardware and firmware are in the main branch
- Algorithm work is in user branches

### CAN
- Communication between microcontrollers and computer is over CAN bus
- CAN broadcasts to everyone, so each node can just choose to receive or ignore a message

### MechE
- If there's one meche who wants to do it then we can just let them do all of it
- Otherwise, we can find an existing vehicle rather than make a frame ourselves
- Or we can just go from scratch

### Firmware Delegation (Suggestion)
- Everyone writes their own drivers independently
- Deal with the freertos and code integration later
- Everyone's code has their own assumptions, so ideally if we force people to make some assumptions before, then it will save headche later