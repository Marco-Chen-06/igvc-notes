End goal (incrementally): 

1. Have 2 picos. One pico sends "u there?" to the CAN bus. 
2. The other pico blinks when it sees a "yea i got msg" on the CAN bus.  It also should have a 10% chance of saying "shut up". This should work with and without the Innomaker because more than one node is on the CAN bus.
3. Connect the Innomaker and learn how to use ROStouCAN and just get that to receive data

Progress:
- [x] 2 picos on the CAN bus both sending CAN messages, and Innomaker receives all of them
- [ ] One pico sends "u there?" every 1 second, the other pico says "yea i got msg" if it sees msg. 
- [ ] Set up ROStouCAN


10/28/2026
I should make progress on CAN and learn about how all picos and the algorithm computer will communicate, and implement it asap.

First thing I want to do: Get a third pico (no debugger) and flash a firmware on it that just sends some message over CAN every time a button is pressed. I also wanna learn how to hook up the reset button on there too.

And then on the 2-pico debugging setup, write code to listen for CAN messages and react in some way, like blinking an LED.

So this means we would need 2 transceiver boards, which I think we technically have that in 701.

And once that's done, we can start looking into ROStouCAN, figuring out where everything is. And then we will test it on this setup.

Also, I've gotta make a slides which ill do right now...

I guess it’s a Linux exercise to git grep the repo until I find rostoucan, don’t do it manually because I know I won’t find anything
