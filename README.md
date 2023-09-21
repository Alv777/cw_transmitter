# CW Transmitter - (🏗️ In Progress)
Use the Raspberry Pi as a CW transmitter. Works on every Raspberry Pi board.

Just get a CW receiver, connect a 20 - 40 cm plain wire to the Raspberry Pi's GPIO4 (PIN 7 on GPIO header) to act as an antenna, and you are ready for broadcasting.

This project uses the general clock output to produce frequency modulated radio communication. It is based on an idea originally presented by [Oliver Mattos and Oskar Weigl](http://icrobotics.co.uk/wiki/index.php/Turning_the_Raspberry_Pi_Into_an_FM_Transmitter) at [PiFM project](http://icrobotics.co.uk/wiki/index.php/Turning_the_Raspberry_Pi_Into_an_FM_Transmitter).
## Installation and usage
To use this software you will have to build the executable. First, install required dependencies:
```
sudo apt-get update
sudo apt-get install make build-essential
```
Depending on OS (eg. Ubuntu Server 20.10) installing Broadcom libraries may be also required:
```
sudo apt-get install libraspberrypi-dev
```  
After installing dependencies clone this repository and use `make` command in order to build executable:
```
git clone https://github.com/Alv777/cw_transmitter
cd fm_transmitter
make
```
After a successful build you can start transmitting by executing the "fm_transmitter" program:
```
sudo ./fm_transmitter -f 100.6 acoustic_guitar_duet.wav
```
Notice:
* -f frequency - Specifies the frequency in MHz, 100.0 by default if not passed
* acoustic_guitar_duet.wav - Sample WAV file, you can use your own

Other options:
* -d dma_channel - Specifies the DMA channel to be used (0 by default), type 255 to disable DMA transfer, CPU will be used instead
* -b bandwidth - Specifies the bandwidth in kHz, 100 by default
* -r - Loops the playback

### Raspberry Pi 4
On Raspberry Pi 4 other built-in hardware probably interfers somehow with this software making transmitting not possible on all broadcasting frequencies. In this case it is recommended to:
1. Compile executable with option to use GPIO21 instead of GPIO4 (PIN 40 on GPIO header):
```
make GPIO21=1
```
2. Changing either ARM core frequency scaling governor settings to "powersave" or changing ARM minimum and maximum core frequencies to one constant value (see: https://www.raspberrypi.org/forums/viewtopic.php?t=152692 ).
```
echo "powersave"| sudo tee /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
```
3. Using lower frequencies (below 93 MHz) when transmitting.

## Legal note
Please keep in mind that transmitting on certain frequencies without special permissions may be illegal in your country, only transmit on frequencies you own. Even though it does not have a lot of power it can still ruin the experience of near people tunned to said frequency.
## New features
* Allows custom frequency and bandwidth settings
* Works on every Raspberry Pi model

Included sample audio was created by [graham_makes](https://freesound.org/people/graham_makes/sounds/449409/) and published on [freesound.org](https://freesound.org/)

This is a fork of the project [fm_transmitter](https://github.com/markondej/fm_transmitter) with some modifications to make plain frequency transmissions.
