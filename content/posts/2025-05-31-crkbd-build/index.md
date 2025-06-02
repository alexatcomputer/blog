+++
title = "Building a Corne Keyboard (crkbd)"
description = "My process of building the split ortholinear Corne keyboard (crkbd)."
+++

Around two months ago I started working on a project to build a split ortholinear keyboard known as the [Corne keyboard](https://github.com/foostan/crkbd) or crkbd for short. It was a difficult process at times but it allowed me to learn a lot about soldering electronics and programming firmware.

Before building the keyboard keyboard I had been using the integrated keyboard on my laptop and a beat up free office keyboard. This was a great upgrade from my previous keyboards and it's hard to go back to a regular membrane keyboard after switching.

This article is not a build guide but a log of my journey of building the keyboard from start to finish. It will outline the mistakes I made along the way and what I would do differently if I could do it again.

## Ordering the parts

I would say that the hardest part of the entire keyboard build was ordering the parts. There were a wide variety of parts that were needed in order to build the keyboard. Below is a list of all of the parts that I ordered to build the keyboard.

- [Corne MX Hotswap v3.0.1 PCB Kit](https://www.littlekeyboards.com/collections/corne-pcb-kits/products/corne-mx-hotswap-pcb-kit-v3?variant=39656127692867)
- [Elite Pi X2](https://www.littlekeyboards.com/collections/mcus/products/elite-pi)
- [128X32 OLED Screen X2](https://www.littlekeyboards.com/products/oled-screen)
- [Corne Analyst Keyboard Case](https://www.littlekeyboards.com/collections/corne-cases/products/corne-analyst-case?variant=39499977949251)
- [Corne Switch Plate Foam 2mm](https://www.littlekeyboards.com/collections/corne-cases/products/corne-switch-plate-foam)
- [Durock Silent T1 (Shrimp) Silent](https://milktooth.com/products/silent-t1)
- [XDA Profile 1X Blank White 50pcs](https://www.amazon.com/Mechkeeb-Profile-Orange-Mechanical-Keyboard/dp/B0BWMP2BR2)
- [Anker USB A to USB C Cable](https://www.amazon.com/Anker-Charger-Charging-Samsung-Galaxy/dp/B0BPCBP15P)
- [SinLoon 3.5mm TRRS Cable](https://www.amazon.com/SinLoon-Auxiliary-Smartphones-Tablets-Microphone/dp/B072TYSV61)

I ordered most of the parts from a shop called [Little Keyboards](https://www.littlekeyboards.com/) because they had a kit of all the parts needed to build the Corne keyboard. I attempted to find all of the parts separately and even looked into a PCB manufacturer to build the PCB but because this was my first ever keyboard build I didn't want to make it any more complicated than it already was.

I went with a silent switches because I knew that I would be using this keyboard in a shared space and I didn't want to be that guy with a super loud keyboard.

There were a couple of things that I ordered that if I were to order them again I would do differently. The TRRS cable that I ordered to connect the two halves of the keyboard is shorter than I would have liked making them too close together. When ordering the plate foam for the keyboard I went with 2mm instead of 3mm to be safe but now there is about a 1mm gap between the foam and the case which limits the amount of sound that it can dampen. I hadn't realized when I ordered the keycaps, but it took around 2 weeks for them to ship which forced me to wait after the keyboard was completed to be able to use it.

Another thing that I wish I had done was ordered a socket and pins to socket the microcontroller to the PCB. This would make it easier to remove it in the case that one of the microcontrollers dies and needs to be replaced. As of writing I have not had a microcontroller fail but I am accepting it as an inevitability.

Next I had to find all the equipment to assemble the keyboard. The build guide from [Josean Martienez](https://youtu.be/vzDTdLaAzXc) gave great recommendations for what equipment to use to solder the keyboard. Below is a list of all of the equipment I ordered to solder the keyboard.

- [YIHUA 926 III 60W Digital Display Soldering Iron Station Kit](https://www.amazon.com/gp/product/B082F1WKP9)
- [Mandala Crafts Lead Free Solder Wire](https://www.amazon.com/gp/product/B0759P8GBZ)
- [Mr. Pen- Heat Tape](https://www.amazon.com/gp/product/B09JLYTZ73)
- [MG Chemicals - 8341-10ML 8341 No Clean Flux Paste](https://www.amazon.com/gp/product/B00425FUW2)

## Building the keyboard

Once I had ordered the parts I was ready to build the keyboard. I started out by setting up a soldering workspace. This was the first time that I've ever soldered something so I didn't have a workspace to safely manage the fumes of the solder. I made my own makeshift setup using my open garage with a fan blowing the fumes outside.

I followed a build guide from [Josean Martienez](https://youtu.be/vzDTdLaAzXc) as well as referencing the [GitHub build guide](https://github.com/foostan/crkbd/blob/main/docs/corne-cherry/v3/buildguide_en.md). The video guide gave me more confidence and reassurance that I was not destroying the components. The first components I installed were the diodes and the microcontroller. Once soldered I was able to test each of the switches of the keyboard with a pair or tweezers using the keyboard input tester from the [QMK Configurator](https://config.qmk.fm/#/test).

Once I had verified that all of the switches were working I installed the hot swap sockets and LED's. Before I started building the keyboard I thought that I would skip installing the LED's onto the board because I would most likely keep them turned off. However, after installing all of the other components I felt like it wouldn't be complete without them. If even one of the pins of the LED is not soldered to the board all of the LEDs will not light up. It took me about one hour to solder the LEDs and then another hour to continuously troubleshoot what LED wasn't soldered to each of the four tiny solder pads. It was very frustrating but rewarding once all of them lit up. To this day I keep the LED's on the keyboard off but I'm still glad that went through with actually installing it.

The OLED was easy to install, the OLED that I ordered came with diodes that I cut off the legs of to create pins for the socket and I just had to solder the socket to the PCB and snap in the OLED.

I had a similar issue when I went to put in the switches as I did with the LEDs. The g and h key would not work. I questioned whether I had even tested those two keys before and if those keys were broken on the keyboard. But it turns out I had just forgotten to solder a side of the hot swap socket to the PCB on both sides.

After installing all of the components it was relatively easy to install the case using the [GitHub build guide](https://github.com/foostan/crkbd/blob/main/docs/corne-cherry/v3/buildguide_en.md#plates--switches) and that was it (at least for the hardware).

## Installing and customizing the firmware

I always had the idea of using QMK and having the firmware of the keyboard in a git repo to track any changes I make. After reading through the [QMK tutorial](https://docs.qmk.fm/newbs) and the other documentation I learned about [external userspaces](https://docs.qmk.fm/newbs_external_userspace). I didn't like the idea of my firmware being a fork of the main [QMK GitHub repository](https://github.com/qmk/qmk_firmware) which had all of the keyboards QMK supported so external user spaces solved my problem perfectly. I forked the [qmk_userspace repository](https://github.com/qmk/qmk_userspace) and I had my [own repo](https://github.com/alexatcomputer/qmk_userspace) with the only keymap I needed.

Since I was using the Elite-Pi microcontroller with the RP2040 chip and not the ATmega32u4, there were a couple of extra steps needed to get it working with QMK. The [keeb.io docs](https://docs.keeb.io/elite-pi-guide) were an incredible resource in explaining what was needed to flash it with QMK firmware. I had to add a line to the rules.mk to convert it in order to map it to the correct pins. I was able to compile the firmware, hit the reset switch twice on the PCB and drop the compiled .uf2 file into the storage device the microcontroller created.

Once I had the basics needed to flash the firmware I was able to start customizing. I started simple by using transparent keys for modifiers on higher layers to make it easier to edit the keymap later. After that I switched the ctrl and alt keys to have the ctrl key on the thumb cluster. So far those are the only changes made, but in the future I would like to add more to the keyboard. I'd like to add home row mods, media keys and a function row in the future and when I do I will write a post about them.

## Learning

Once the keycaps were finally shipped and installed I started my journey of learning to type on my new keyboard. I never formally learned how to touch type and instead just developed a muscle memory which worked for me. This lack of proper learning really hindered my ability to properly learn where to put my fingers. I started using [keybr.com](https://www.keybr.com/) to get the basics down. Since the keycaps were blank I printed out the keymap layers using the [QMK configurator](https://config.qmk.fm/#/print) to reference when needed.

Just as I was starting to develop the muscle memory of using the keyboard I had to write 4 essays for final exams. I had the goal to use the keyboard to type up all the essays and I was able to do it. This really helped me to get used to the layout and where all the keys were and it helped me to become more proficient on the keyboard.

It was a slow and frustrating journey, and I still don't think that I am at a level I would like to be at. I still struggle in finding where the symbols are and have the reference the keymap layers sheet I printed out from time to time.

Now when I go back to a regular keyboard it takes more time for my muscle memory to kick back in. Having the arrow keys on the home row has rewired my brain and having the reach to the corner of the keyboard to use them is more infuriating now than ever. But I do think that I am a better typist after learning the new layout. I have noticed that I am keeping my hands on the home row more even when I'm on a regular keyboard.

## Concluding thoughts

Overall, I'm really happy that I took on such a project. It was really fun to learn about something that I had no experience in and have to build something that is so unique. This won't be the last keyboard I ever build because there is so much more that I haven't explored.

In the future I would like to build a keyboard from scratch which would require me to source all of the components myself and order the PCB through a PCB manufacturer. I'm glad I didn't do that for my first keyboard build but now that I have the experience I think that I am ready to do it.

All that being said, this is a great project that I believe anyone with enough time on their hands and willingness to learn can do and have a good time doing it.