# UP/Down Timer Report

## Introduction:
This week we built a timer that is capable of counting down or up from 60 minutes and displaying the 60 minutes with decimal numbers, not the hexadecimal numbers used in previous versions. The changes made to the code and hardware consisted of adding new state machines, adding some new physical wires to our circuit board, reorganizing the GPIO pin allocation, and adding the multiplication and division capability to our RISC-V processor on the FPGA.

## Plan:
For the initial process, we had to clone the project 4 repository from GitHub.com. This particular ‘cloning’ was different in the fact that we opened a browser on the Raspberry Pi and downloaded the zip to the desktop instead of merely using the command palette from VSCode. Furthermore, like past projects, we used GNU Make which controls the generation of executables of our program. 
\
Next, we had to make changes in our .pcf file--or packaged collaboration file extension. This extension allows for multiple documents to be combined, thus, we were able to check our particular pin, pin 25, and see--by inserting and removing--that the counter was, in fact, counting up and down.
\
Moreover, we had to remove the decimal points as well as make the colon in the display blink once a second. For the former, we believe the easiest method was just zeroing, or turning them off.
\
The latter required us to make a change with ‘second_toggle.” That is to say, we wanted it to be lighting up only ¼ of the time, but we only wanted it to be doing that when  ‘second_toggle’ was high, which ‘second_toggle’ switches between 0 and 1 every second. 
## Implementation :
Much of the logic in the implementation of our project relied on the use of second_toggle. This is a signal that is being inverted every second, so that we can keep checking this signal over and over again in software to know when a second has passed.
\
We utilize the second_toggle signal in the state machine in firmware.c to make the colon blink every second. The state machine is the same as what the digits are being activated in, so that the segment is only activated once every four states, perceiving a certain level of brightness. With the second_toggle signal being in place of the enable state, we are making the colon only display/blink once per second.
 \
In order to display the time in decimal minutes and seconds using integer division and modulus we needed to enable these operations in the top.v file.
\
Once this was done, we were able to uncomment the block of code in firmware.c  which utilizes those operations in order to calculate the correct minutes and seconds.
## Results:
This project we ran into virtually no problems. Our biggest problem was when we attempted to make the files it would often get hung up, and we would have to abort and try again. We were able to verify that our project worked correctly by looking at the 7 segment display and watching it count up or down. When removing the wire connected to pin 25 the display would count down, and with the wire inserted the display would count up. We chose to remove the wire because it did the job without writing more code for the software to handle when the display counts up or down. 
## Conclusion:
This system created is rudimentary, but can and probably is used in part or similarly to alarms and timers that sit on our nightstands. We could enhance this system to create a similar alarm system whereby once the desired time is reached the 7-segment display could blink and an attached alarm hardware (from adafruit) could be triggered. 
