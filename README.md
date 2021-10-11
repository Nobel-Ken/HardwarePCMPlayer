# [Hardware] PCM8³Player
The PCM8³Player is a completly discrete hardware module designed to play back PCM audio clips. It is constructed of TTL logic parts and contains **no** microprocessors or microcontrollers in its design. It can play back 8 different PCM audio clips at a resolution of 8-bits at a sample rate of 8kHz (hence the name PCM***8³***Player).

![asdf](https://user-images.githubusercontent.com/17792367/136730472-d3723425-0bc8-43a6-8f51-a039c1a7663e.jpg)
![asdasd (2)](https://user-images.githubusercontent.com/17792367/136730481-324cb973-8789-4cba-b0d9-a50652f755bc.jpg)

### Design
The design of the PCM8³Player revolves around its 32k EEPROM. This EEPROM stores the audio dates encoded as a stream of unsigned 8-bit samples at a sample rate of 8kHz. As a 32k EEPROM, it takes 15 bits to adress a memory location. For the 8³Player, this is split, with the lower 12 bits going to a 12-bit binary counter (3 74LS161's cascaded) and the upper 3 bits going to the output to act as the 3 "bank" select pins. This is what allows the user to select between the 8 diffrent clips. Because of this design each sample "bank" is 4096 samples long, which at a sample rate of 8khz, equals a clip lenght of a little over half a second.

![asdasdasd](https://user-images.githubusercontent.com/17792367/136730482-9491715f-46de-4d10-a8ca-2c18980ad210.jpg)
