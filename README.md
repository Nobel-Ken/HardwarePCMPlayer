# [Hardware] PCM8³Player
The PCM8³Player is a completely discrete hardware module designed to playback PCM audio clips. It is constructed of TTL logic parts and contains ***no*** microprocessors or microcontrollers in its design. It can playback 8 different PCM audio clips at a resolution of 8-bits at a sample rate of 8kHz (hence the name PCM***8³***Player). The shown player has been completely hand-soldered on perfboard, however, the design can easily be replicated as a PCB as well.

![asdf](https://user-images.githubusercontent.com/17792367/136730472-d3723425-0bc8-43a6-8f51-a039c1a7663e.jpg)
![asdasd (2)](https://user-images.githubusercontent.com/17792367/136730481-324cb973-8789-4cba-b0d9-a50652f755bc.jpg)

### Design
The design of the PCM8³Player revolves around its 32k EEPROM. This EEPROM stores the audio dates encoded as a stream of unsigned 8-bit PCM samples at a sample rate of 8kHz. As a 32k EEPROM, it takes 15 bits to address a memory location. For the 8³Player, this is split, with the lower 12 bits going to a 12-bit binary counter (3 74LS161's cascaded) and the upper 3 bits going to the output to act as the 3 "bank" select pins. This is what allows the user to select between the 8 different clips. Because of this design, each sample "bank" is 4096 samples long. At a sample rate of 8khz, this equals a clip length of a little over half a second. 

The 8kHz sample rate is achieved using an onboard 555 timer set up as an oscillator. This is hooked to the 12-bit counter via a jumper, which allows the user to bypass the internal oscillator at any time (to, for example, use an external oscillator to pitch-shift the played back clips). 

Playing back clips is triggered via a high pulse on the trigger pin. This sets a latch that enables the counter, allowing the audio clip to be played. Once the counter reaches the end, its ripple output is used to reset the latch, thus ending sample playback. The digital PCM data is put through a DAC which is then sent to the output for the user.

![8cubedPlayer](https://user-images.githubusercontent.com/17792367/136813825-6187d8ff-2bd1-4b45-9fb4-2fe39431ac7b.png)
![asdasdasd](https://user-images.githubusercontent.com/17792367/136730482-9491715f-46de-4d10-a8ca-2c18980ad210.jpg)

### Development
Back in December of 2019, I had started working on designing a digital drum machine completely from scratch. For the machine, I needed a way to playback audio. Around this time, I had a bit of an obsession with digital audio; I had decided this drum machine project was the perfect excuse to learn more by designing and building my own hardware audio clip player from the ground up. 

After a little bit of thinking, I had come up with an idea for doing this using a few binary counters that fed addresses to an EEPROM memory chip. While my idea to do this was straightforward, a bunch of stuff got in the way from actually starting, but eventually, in February of 2020 I had started and soon had a prototype.  

(The audio clip it's playing is one of my friends saying "Bruh" which turned out to be the perfect length for testing) 
https://user-images.githubusercontent.com/17792367/136837612-8fe6a32f-75a2-41ab-bde9-89fab733bce3.mp4

The circuit had worked! And not only did it work but it worked surprisingly well! I had anticipated much worse sound as the sample resolution and the sample rate (8-bits at 8kHz) are rather low for audio standards (for context CD-quality audio has a resolution of 16-bits and a sample rate of 44kHz), but apart from a bit of grit in the sound (which would have been perfect for the original application as a drum machine), it wasn't that bad.

The only glaring flaws in the design were some noise picked up by the breadboard and noise caused by a lack of decoupling capacitors. While the first was fixed when the circuit was soldered to a perf board, the latter still is a minor problem as there ended up being no room for decoupling capacitors when all was done and dusted. Speaking of the perf board the final step was soldering it all onto one. 

![IMG_20200326_224745](https://user-images.githubusercontent.com/17792367/136842504-7c90284c-510c-463d-b222-2745d545e585.jpg)
![IMG_20200326_223100](https://user-images.githubusercontent.com/17792367/136842513-a636353c-6f1e-42d1-acf0-29f14fee5a8f.jpg)

And Voilà, it's done! This was one of my favorite projects to work on as it combined two things I like a lot, digital logic and audio. This project has taught me a lot, considering it was the most complex circuit I had ever designed and constructed at the time.

Also to address the obvious question, yes, I know an Arduino and an SD card could have achieved the same thing in a much easier way, and had this been a commercial product I was working on instead I would have gone down that route. But this isn't a commercial product, and there is nothing that impressive or new about getting a microcontroller to playback audio, which is why I went down the path of doing everything discretely with TTL parts (not to mention how much more you actually learn doing it this way). 
