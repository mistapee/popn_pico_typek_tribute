gerbers added - see bottom for ordering and parts infos

Wowechina's Gen 1 Popn' pico just hit all our needs initially, cute but completely functional to play properly so we were just goint o fork that project. We hit some snags and over time the only thing that has remained the same is the size/layout. Over time students will be writing their own firmware and initially I used Gp2040-CE but it feels right to appreciate where we started.



The MistaPee Ver:
![popn1 (1)](https://github.com/user-attachments/assets/ba93bcf3-a9f1-4a0a-ac75-a106108d1709)


As with the rest of my stuff up at the moment I'll finish this off later but some useful points
changes and whys:

- removed USB C port to just use the one supplied - explaining how to hand solder those either encourages going against what we would explain as good soldering habits, or just caused doubt on their reliability. the port itself also costs as much as a pico

- we seemingly killed 3 pico's soldering the test points through the PCB so no more of that, for educating through encouraging it's important things are clear 

- removed the side facing LEDs, so many reliability issues especially in sourcing different batches and some were harder to solder than others

- switched to fewer LEDs and to 5050's, at the time of making these the 5050s were far more available and way way cheaper.

- the nature of the pads for the 4020s and the tight routing for so many meant that the PCBs in the spec they were ordered did not handle repair jobs for long, so we spread the traces out although that's not really an issue any more what with changing the LEDs

![popn2](https://github.com/user-attachments/assets/f3970954-1cdf-4b0f-aeb4-134f2496eed0)


  these changes met our/the students needs far better, easier to have a solid and cheaper build to get on with exploring
  i insist on using decent fight box key caps, they looked and felt so perfect on the wowechina gen1, trying to cheap out on this wasn't worth it. as other posts have said we don't can't and won't 3D print, but cheap caps have injection molding tags and whatnot which can't be accepted. they don't fit visually on this one as well as they did on the wowechina gen1 and really i still prefer the shape of that one, but it seemed right as we moved furtrher from it to try our own thing. Also I've no been able to get a Type K imported yet.


Popn Pico Firmware (see underneath for changes needed to compile for our controller as the GPIO pins are different - it's a good way to start to understand it)

Features:
* 1000Hz polling rate.
* HID lights (9 button lights and Logo RGB).
* RGB rainbow effects.
* Light brightness control.
* Light fade in/out control.
* Configuration save.
* Customizable through board_defs.h

  
The original inspiration
  ![20251213_195752](https://github.com/user-attachments/assets/2895e428-a98f-48cd-848a-0667338dd2c3)

go check out the original, it really works for me, play in bed, pizza to one side... bliss


in board def find this section and change to this:

/* A button consists of a switch and an LED
   9 main buttons + 2 aux buttons. */
#define BUTTON_DEF { \
    {20, 21}, \
    {18, 19}, \
    {16, 17}, \
    {10, 11}, \
    {8, 9}, \
    {14, 15}, \
    {12, 13}, \
    {4, 5}, \
    {6, 7}, \
    {2, -1}, \
    {3, -1} \
}

#define RGB_LED_PIN 22
#define RGB_LED_NUM 3
#define RGB_LOGO_LEDS {1}
#define RGB_RAINBOW_LEDS {0, 1, 2}



---

ordering:

on JLC or whatever it is all default settings MOQ of 5 units - BUT - the current top plate does not contain copper layers so you have to do some something extra to order.
The process to do the copper art is very involved and if I couldn't be bothered to be very smooth and fluent with it then it's no good showing others, I figured the board would be strong enough anyway and there would likely still be some light differences. Anyway - the PCB company will contact you confused and tell you there's no copper layer, delaying your order, so i just put in the order info that i am aware it is just mask and a small bit of silk screen on the board with no copper. as it is, it actually works quite well, but, i think i could add a copper layer in but not simply to thicken the design as is but as seperate design elements of its own giving it some additional depth - if you're used to copper fill regions and the rules it follows to adjust after you have changed other elements it might become apparent how manual routing traces and polygonal fill regions could be used as a drawing tool of sorts. i'll add it here once i've had a go.

parts though! 
pico
9 MX keys (footprint is full size not low profile or anythinbg) - anything linear and not clicky should do, i use a lot of Gateron, but recently been tried OutEmu Silent that don't thud when they bottom out.
9 hotswap sockets
9 2835 white LED - one for each key - sometimes(?) seemingly very offset contacts underneath heavily biased to one side that you need to be aware of and adjust for
3 5050 RGB LEDs - there's different versions but i've not had it make a difference, finding them loose seems difficult here but they're plentiful and cheap on reels, they're quite easy to desolder
2 tactile switches (4.5x4.5 width, height 7mm. 
10 220 resistors as it's one per key and one between RGB data GPIO and first LED
screws/nuts - amazon happened to have packs of 150 nylon 12mm m3 bolt and nut, depends if you're printing a case or putting the bolt through rubber feet etc.


it is mosty obvious, with the tactile ssitches and the pico lightly solder a single point so that you can melt and cool that one contact to make finer adjustments for alligning stuff. 

the was a reason the pico was put on the back, despite plenty of space up front, i have completely forgotten why. the pico goes on the back though, i push the tip of the iron in each indent to get the diffierent surfaces warm and then tap it with a very fine solder - i try not to drown it, there's no need for it to cover or go dowm the hole, even heat first just a little solder makes a nice connection. 

For the hotswap sockets while it is important to have electrical connection the solder will be putting in some work as an anchor holding them to the board. the cheaper sockets i currently have actually have really good access through the metal socket and to the pads to get solder right in, then i'll flow some around it a bit too. The branded ones that were poor on access I found wee best applied with some solder put on a put, adding the socket and warming it to sink in to it - then flooding it. 

for the resistors, as they are tiny, even tweezers can fall short - i dab solder on one of the contacts on the pcb and as i get the resistor close melt the solder and it'll pull the resistor in. if it's not very straight don't try to fix it right away, go to the other end and chances are the heat will spread through it melt the original contact allowing you to pivot and done, like ballet or something, ya fancy fella.

putting the keys in the plate support the hole as you clip them in *thuunk* and you'll need to keep a bit of an eye on the pins linign up with the sockets and squeezing the layers togeher evenly - it's far more likely if you have to take it apart that you'll be leaving the eys in the plate, the vulnerable bit to be aware of are those pins. 

the nylon bolts i used, if you used them, don't tighten them up as it'll bend the pcb, just done up so they grip as it stops the pcb layers coming apart. if the gap was exactly 2 or 3 washers i would have used washers, but 3 is too many and 2 looks stupid doing nothing and flopping abaout. half a washer is quite a dramatic difference. 


when you're ready hold the bootsel button, plug it in, let go of the button and there's your drive for dropping your firmware on

