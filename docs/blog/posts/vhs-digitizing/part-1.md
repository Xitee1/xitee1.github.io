---
comments: true
date:
  created: 2025-10-12
  updated: 2025-10-12
draft: true
---
# VHS-Decode - Part 1

**This tutorial is exclusively for capturing VHS tapes**

This tutorial (or rather blog) shows you the absolute basics on how to do your very first video-only capture with vhs-decode.
Capturing audio and improving the quality will come in later parts of this blog (if I manage to understand it :laught:).
It's meant for absolute beginners, although it's assumed that you have some basic technical understanding + skills and know how to use the terminal in Linux.

## Requirements
### Skills
- Basic soldering skills
- Basic Linux & Terminal understanding (includes knowing common commands, e.g. changing directory, moving files, ...)

### Main parts
- PC with two spare PCI slots and Linux as OS: For beginners preferred Linux Mint or at least Debian based (Linux Mint is based on Ubuntu which is based on Debian), most other distros work too, but in that case you should really know your distro.
- VCR (**V**ideo **C**assette **R**ecorder) (your VHS player)
- Optional: TV/Monitor for the VCR (just for viewing the tape during capture)
### Miscellaneous parts for vhs-decode
- Soldering iron and belonging tools
- CX Card(s) (you'll need two of them to capture video **and** audio because they're separate for VHS, but in this first test we're only going to capture video, so one is enough for now)
- BNC Female Jack Bulkhead To SMA Male SMA Plug ![[Pasted image 20251012173919.png]]
- SMA Male to SMA Male (or two separate male cables with no connector at the other end, but I found it's easier to find a male to male cable and just cut it in half)  ![[Pasted image 20251012175056.png]]
- RG316 BNC Male to BNC Male ![[Pasted image 20251012175726.png]]
- BNC Female Right Angle 90 Degree Plug (make sure they look like in this image, there are lots of different variants and this is the one that fits to the CX cards) ![[Pasted image 20251012175701.png]]
- 10uF Capacitor, preferred ceramic but if you have a spare electrolytic it'll do, but there you need to be aware of the polarization (or just directly go with the amplifier from the ko-fi store, but as of writing this, I haven't fully understood it myself and are just in the first capture stage)![[Pasted image 20251012180347.png]]

To make it clear if you're a bit overwhelmed with all the connectors: These are really only for convenience. Theoretically, just a long enough bare coaxial cable would be enough, the connectors are just for convenience to allow you unplugging it and integrating the amplifier (you don't need to know about the amplifier yet).

For all the cables you should get ones with 50 Ohm (usually specified in the product title or description).

For the length, you should just measure how much you need and order ones as short as possible to improve the capture quality (although you should still add a bit extra just in case).

## Start
Okay, so let's start.
If you're reading this and haven't ordered your parts yet or you currently wait for them to arrive, keep on reading to get a better understanding of how it works. It'll help reading this multiple times, with some time between. You can also do some preparation already.

First, find a place to put your VCR and (preferred dedicated) capture PC.

Take a note of your VCR model name.
Remove the cover from your VCR (the screws are on the sides and back most of the time).

#### Finding the test point
For finding the test points, you should follow the official WIKI. As said, in the first step, we're only going to capture video so we just need to find the video test point, although it won't hurt searching for the audio test point too. Note that if your VCR does not have Hi-Fi audio support (most of the time it's written on the tape cover on the front of your VCR), you won't find a audio test point because this test point is ONLY for capturing the Hi-Fi (better quality) audio. Not all VCRs support that and not all tapes have Hi-Fi audio in the first place. That means if your tape doesn't have Hi-Fi audio the Hi-Fi test point will be completely useless even if your VCR has one and you'll need to capture the standard way with the standard audio output at the back of the VCR.

VHS-Decode links:
- General info: https://github.com/oyvindln/vhs-decode/wiki/RF-Tapping#test-point-names
- List of already found test points (check if your model is in there): https://github.com/oyvindln/vhs-decode/wiki/004-The-Tap-List
- Reports (check if your model (or manufacturer) is in there to get more info about your model): https://github.com/oyvindln/vhs-decode/wiki/VCR-reports

If you can't find the test points by looking at the PCBs inside of the VCR, search the web for a service manual for your specific model.
It's not that easy to read them if you haven't read service manuals before, but it can definitively help. For example in my case there was a white connector with 6 pins on the board, but only labelled with a "cryptic" name. I found it in the service manuals and there was also the description what each pin does, one of them was the test point that we need.
If your service manual contains a troubleshooting section, that can be very helpful too.

Sadly, it's not always easy to find service manual. If you have luck, you directly find it when searching google for your model number and writing `service manual` behind it.
You'll have issues finding it most of the time if you have a re-branded model (no main brand like JVC, Sony, ...).
In my example I have an `AGFAPHOTO DV 18909R` and I couldn't find a service manual at all.
After opening it up and removing the whole tape unit, I saw another model number printed on the mainboard. This revealed the actual manufacturer (which was Daewoo). That still wasn't enough because that model number from the mainboard didn't really existed, but luckily when typing it in google lead to a normal user manual with a VCR that looked idendical to mine. And it contained the actual model number of the unit itself. All I had to do was type in this newly found model number and - I got my service manual!
All I want to say with this is, it's very likely that your service manual is somewhere out there, you just need to hunt it down.

If you still can't find the test point, you can create a post in the vhs-decode subreddit or ask for help on the Discord server.
But if you do so, you should have your service manual ready to get the best help.

#### Wiring
You've found your test point.

Get the SMA male cable with no connector on the other end. Solder that end to the capacitor.
Use the official WIKI to find out how to connect the other end of the capacitor to your test point.
Now you have a SMA male connector that goes to your test point.
Use all the other cables to extend it and to get a final BNC male output.

#### CX Cards
First find out what model you've got and if it is good: https://github.com/happycube/cxadc-linux3/wiki/Types-Of-CX2388x-Cards
They even ship different models if you order multiple at once. For me, one had the cx23883 and the other the CX25800 chip.

Now we're going to do the following mods:
- [RCA to BNC replacement / adding](https://github.com/oyvindln/vhs-decode/wiki/CX-Cards#rca-to-bnc-replacement)
- [C31 Removal / moving](https://github.com/oyvindln/vhs-decode/wiki/CX-Cards#c31-removal)

In my case I'm using the 3rd connector (and not replacing the middle connector) because one of the cards already had the hole. For the other one, I'm going to drill the hole myself.
After having the BNC connector installed, do the C31 removal (or move it to the other pad if you're using the 3rd connector like I did).

Because I will do the clockgen mod later anyway (which I really recommend to avoid sync issues) and just want to see if it's working at all right now, I'm not going to do the crystal replacement mod.

After your card is ready, install it to your capturing PC.
I suggest not connecting the previously made BNC male output from the VCR yet.

## The software part
1. Install driver
2. check if driver is loaded by checking if cx card is detected
3. find the correct vmux input: https://github.com/happycube/cxadc-linux3/wiki/Types-Of-CX2388x-Cards#cx-white-card-old-rca-s-video
4. connect BNC male output to cx card
5. ffplay
6. run some driver scripts?
7. first capture to .u8
8. .u8 to .tbc
9. analyse (ld-analyse)
10. export