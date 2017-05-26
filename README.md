# Power on STBs with blank video

## Description

If you have a PVR like SageTV or MythTV where you are recording from Set Top Boxes (STBs) that
you rent from your cable company, you know there are times when the STB powers itself down due
to inactivity timeouts or upgrades/reboots of the STB by the cable company.

This script checks each video device and if it appears that the signal is blank, sends the
power on command to the STB.

I've generally found this useful to run via cron at 25 and 55 minutes after the hour, so that the STB
is checked right before a recording may start. If the video device is already in use it will
just skip the check. Don't run this script as root - use another user who can read from the video devices.
On some Linux distros any user in the `video` group can do this.

Thanks to Evuraan who came up with this idea.
See his blog entry and `check_stb` script: [How to ensure Set-Top-Box (STB) is Powered On?](http://evuraan.blogspot.com/2008/01/how-to-ensure-set-top-box-stb-is.html) for details.

My main modification to his script was to support multiple video devices.

## Installation

* Make sure `jp2a` and `ffmpeg` are installed on your system
* Download `blank_check`
* Make it executable (`chmod 644 blank_check`)
* Edit the three items in the Configuration section at the top of the script for your installation. You will need to:
 * Update the space separated list of video devices to match the ones on your system
 * Choose to log to the console or syslog
 * Supply a command that will send the power on command to an STB in your environment. The video device is
   passed as the first argument to this command and can be used by the script to determine which device
   needs to be powered on.
* Add to cron to check periodically

