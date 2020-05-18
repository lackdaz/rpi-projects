# Secure Shell (SSH)
SSH allows to access your rpi remotely and a larger convenience of not having to attach keyboard and mouse inputs to the rpi. You have to be relatively comfortable the command line interface(CLI).

| Pros 	| Cons 	|
|-------------------------------------	|---------------------------------------------------------	|
| No need for keyboard / mouse inputs 	| Relative comfort with CLI and their native text editors 	|
|  	| Security (change the default password) 	|

### Setup
#### (with MacOSX)
1. Go to terminal(rpi) and type:

      `ifconfig`

      note the `inet` address, or

      `ping raspberrypi.local`

      on terminal(MacOSX) if you are on the same network
2. Access the raspi config GUI by:

      `sudo raspi-config`

      and enable SSH through
      `5. interfacing options` > `P2 SSH` > `Enable: Yes`.
3. This is a really good time to change your default password if you haven't done so already - `1. Change User Password`. (__Note__: This is how rpis get hacked).

      After you are done, reboot by `sudo reboot`.
3. After reboot, SSH into your rpi by typing

      `ssh pi@<ip-address>`

      e.g. `ssh pi@192.168.1.110` and you're in!

### Basic Commands
| Index 	| Command 	|
|-------------------------------------	|---------------------------------------------------------	|
| vim text editor | `vi`	|
| reboot rpi | `sudo reboot`	|
| shutdown rpi | `sudo halt`	|
| cancel/shutdown ssh | `ctr-d`	|

### X-forwarding
X-forwarding allows you to access GUI interfaces on your RPI on a remote client [(Read More)](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md). They used to ship with MacOSX's X11 but was [discontinued](https://support.apple.com/en-us/HT201341) from May 2017 :poop:

For Troubleshooting help:
1. [How to configure X11 forwarding and  debug XAuth](https://unix.stackexchange.com/questions/12755/how-to-forward-x-over-ssh-to-run-graphics-applications-remotely)

#### Steps
1. Download and install X-Server from https://www.xquartz.org/
2. Use xterm:

      `ssh -X pi@<ip-address>`

      The -X (capital X) option to ssh enables X11 forwarding for your client, and you can make this the default (for all connections or for a specific conection) with `ForwardX11 yes` in `~/.ssh/config`.
3. Run any graphical UI like:

      `idle &`

### Password-less SSH login
1. First generate a rsa key via `ssh-keygen`
2. Then copy your key to your remote pi via `ssh-copy-id pi@<replace-with-static-ip-address>`, key in your remote pi user's password and voila!
