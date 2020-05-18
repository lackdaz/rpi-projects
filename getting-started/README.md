# Getting Started

## Bill of Materials
To start off you will need a few important things:

1. A Raspberry Pi of any model

    The latest being the Model 3 B+, just note that most peripherals are not compatible with the Pi Zero (so it's a great place to start). I would highly suggest starting with the model 3 and above because they are faster and comes with an inbuilt network adapter.

    [Element 14](https://www.element14.com) is the exclusive distributor for the board and you can find these on their website. **Pro tip**: if Element 14 offers free delivery in your locale - you can get these direct from them if you buy it as a 'business entity'. Resellers suck.

2. A micro-USB power supply that supplies at least 2A

    These are hard to come by, but they should be available from Pi resellers. I got mine from [taobao](https://item.taobao.com/item.htm?spm=a1z09.2.0.0.5d832e8dxS1L6l&id=529019228089&_u=d2nm6urldac7) at about SGD3.

    You can also try out amazon or aliexpress.

3. An micro-SD card with at least 8GB of memory, with an SD card adapter

4. A monitor with HDMI input cable, a spare keyboard and mouse (for installation)

    The keyboard is used only for installation and will not be needed after you are connected to wifi and you are able to SSH.

    **Pro-tip**: You can use a bluetooth keyboard for the initial installation but remember to disconnect after you are done because the raspbian bluetooth daemon tends to be rather 'sticky'.

## Step-by-step Instllation (MacOSX)

You can install Raspbian - the OS onto your SD through [NOOBS](https://www.raspberrypi.org/downloads/noobs/) or [Etcher](https://etcher.io/) - but I highly recommend using NOOBS because of some forward compatibility issues when doing it via Etcher - particularly when upgrading your distribution on the Model 3 B to 3 B+. You can read more [here](https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=212452).

To start off:
1. Download NOOBS [here](https://www.raspberrypi.org/downloads/noobs/)
2. While NOOBS is downloading, insert your micro SD to your card adapter. Before reading your SD, check that the adapter lock switch is in the ["unlocked" position](https://kb.sandisk.com/app/answers/detail/a_id/1102/~/sd%2Fsdhc%2Fsdxc-memory-card-is-write-protected-or-locked).
3. We will be using `diskutil` to format the SD card. So fire up the terminal (`cmd + space` and type 'terminal'). In the command prompt, type `diskutil list` to view all your connected volumes. Look for your connected device - it should be labeled `NO NAME` with the corresponding size of memory that you bought. Alternatively, you can use type `diskutil list external physical` to only surface external connected physical devices.

4. Take note of the disk number - as seen `/dev/diskX` where `X` is your disk number. It is __very important__ to not make any mistakes with this as you can be reformatting your local hard drives.

5. Reformat the SD card by with typing `diskutil eraseDisk FAT32 RASPBIAN MBRFormat diskX` into the command line, where `X` is your corresponding disk drive as noted in 4. You can also rename your volume to any name by replacing `RASPBIAN`, ie `diskutil eraseDisk FAT32 RaspberryPi MBRFormat disk2`. If your SD card is under 64GB - you can reformat your disk with `FAT` instead of `FAT32` format.

6. After NOOBS has downloaded, extract the files into your SD card root directory. Your root should not consist of only one folder and should look something like [this](https://imgur.com/a/a8vG1fx). Dismount the card.

7. Insert the micro SD card into your Raspberry Pi, connect the HDMI cable and finally your power cable. Switch it on!

8. You should see a GUI pop up for the NOOBS version that you've installed. Select Raspbian and click on install (top left). This is going to take a while so go get yourself a coffee.

If all goes well, Raspbian would be installed and you can now start hacking away with your Raspberry Pi!

9. Check how much space you have left with `df -h`

Here are some super useful utilities that I install with my mint Raspbian:

1. matchbox-keyboard - an on-screen keyboard that allows you to type using your mouse. Tends to double tap with some mice so be careful.

2. x-screensaver - disable that annoying screen blanking after 15 mins.

3. git

## Static IP Address
1. `sudo vi /etc/dhcpcd.conf`, paste the following after the # example and save the file.
    ```
    interface eth0

    static ip_address=192.168.0.2/24
    static routers=192.168.0.1
    static domain_name_servers=192.168.0.1

    interface wlan0

    static ip_address=192.168.0.2/24
    static routers=192.168.0.1
    static domain_name_servers=192.168.0.1
    ```

2. Reboot the pi via `sudo reboot now`
