# xnohands_daemon
A simple bash script to automatically start xnohands when a Wacom tablet is detected.

## Installation
[XNoHands](https://sourceforge.net/projects/xournal/files/xnohands/) must be installed prior. This script does not come with XNoHands.

Copy the `xnohands_wait_off`, `xnohands_wait_on`, and `xnohands_start_daemon` files to `/usr/local/bin`

As root, run:

    chmod +x /usr/local/bin/xnohands_*

Finally, add `xnohands_start_daemon` to your `~/.xprofile` file to automatically start the daemon when logging in.

## How it works
The daemon is started by `xnohands_start_daemon`. This script looks for a Wacom tablet in the output of `xinput` and start the appropriate daemon: `xnohands_wait_on` or `xnohands_wait_off`. 

`xnohands_wait_on` will sleep until it finds a Wacom tablet in `xinput`. It will check every second. When a tablet is found (plugged in), it triggers `xnohands` and `xnohands_wait_off`, and exit.

`xnohands_wait_off` will do the exact same thing, but instead it will wait for the tablet to be unplugged. When the tablet is unplugged, it kills `xnohands` and triggers `xnohands_wait_on`.

The loop repeats until it is explicitely killed (`killall xnohands_wait*`).

## Contact
This script was written by Corentin Moevus (c.moevus@gmail.com) and is officially located on [GitHub](https://github.com/cmoevus/xnohands_daemon)
