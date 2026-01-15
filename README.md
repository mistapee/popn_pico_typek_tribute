Wowechina's Gen 1 Popn' pico just hit all our needs initially, cute but completely functional to play properly so we were just goint o fork that project. We hit some snags and over time the only thing that has remained the same is the size/layout. Over time students will be writing their own firmware and initially I used Gp2040-CE but it feels right to appreciate where we started.

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

  ![20251213_195752](https://github.com/user-attachments/assets/2895e428-a98f-48cd-848a-0667338dd2c3)

go check out the original, it really works for me, play in bed, pizza to one side... bliss


>> in board def find this section and change to this:
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
