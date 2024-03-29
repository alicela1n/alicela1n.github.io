---
layout:	post
title: "Restoring and updating iOS devices from Linux with iDeviceRestore"
date:  2020-01-07 13:14:30 -0800
---
# **Introduction**
You may be a Linux user, but you may have an iPhone as well. Occasionally there will be times when you'll need to restore and update your iPhone. You may think that because you're using Linux you are unable to restore or update your iOS device without a virtual machine or dualboot. Thankfully this is not true. Thanks to the developers behind libimobiledevice there are new tools to do the restore and update process directly from Linux. The tool is called idevicerestore! 

# **Installation**
Thankfully for Arch Linux users it's already in the [AUR](https://aur.archlinux.org/packages/idevicerestore-git/)! On Ubuntu and other distros that use the apt package manager you can install it using this [script](https://gist.github.com/stek29/2d3d0e2f2d1c14f8be68ce3a296585e9) although I cannot confirm this script works so beware that I haven't tested. Another options is compiling the [source code](https://github.com/libimobiledevice/idevicerestore).

# **Using**
Typing ``idevicerestore`` in the terminal will show you the syntax.
```
Usage: idevicerestore [OPTIONS] PATH
Restore IPSW firmware at PATH to an iOS device.

PATH can be a compressed .ipsw file or a directory containing all files
extracted from an IPSW.

Options:
 -i, --ecid ECID  Target specific device by its ECID
                  e.g. 0xaabb123456 (hex) or 1234567890 (decimal)
 -u, --udid UDID  Target specific device by its device UDID
                  NOTE: only works with devices in normal mode.
 -l, --latest     Use latest available firmware (with download on demand).
                  Before performing any action it will interactively ask to
                  select one of the currently signed firmware versions,
                  unless -y has been given too.
                  The PATH argument is ignored when using this option.
                  DO NOT USE if you need to preserve the baseband (unlock)!
                  USE WITH CARE if you want to keep a jailbreakable firmware!
 -e, --erase      Perform a full restore, erasing all data (defaults to update)
                  DO NOT USE if you want to preserve user data on the device!
 -y, --no-input   Non-interactive mode, do not ask for any input.
                  WARNING: This will disable certain checks/prompts that are
                  supposed to prevent DATA LOSS. Use with caution.
 -n, --no-action  Do not perform any restore action. If combined with -l option
                  the on-demand ipsw download is performed before exiting.
 -h, --help       Prints this usage information
 -C, --cache-path DIR  Use specified directory for caching extracted or other
                  reused files.
 -d, --debug      Enable communication debugging

Advanced/experimental options:
 -c, --custom     Restore with a custom firmware
 -s, --cydia      Use Cydia's signature service instead of Apple's
 -x, --exclude    Exclude nor/baseband upgrade
 -t, --shsh       Fetch TSS record and save to .shsh file, then exit
 -k, --keep-pers  Write personalized components to files for debugging
 -p, --pwn        Put device in pwned DFU mode and exit (limera1n devices only)

Homepage: <http://libimobiledevice.org>
```
For restoring to the latest iOS version which is the thing most people will do, you simply do ``idevicerestore -e -l``
```
~ ❯ idevicerestore -e -l
Found device in Normal mode
Identified device as n71ap, iPhone8,1
The following firmwares are currently being signed for iPhone8,1:
  [1] 13.3 (build 17C54)
Select the firmware you want to restore: 1
Selected firmware 13.3 (build 17C54)
Downloading firmware (http://updates-http.cdn-apple.com/2019FallFCS/fullrestores/061-61296/1EFCEDB4-179E-11EA-B3B3-D73E73E9483A/iPhone_4.7_13.3_17C54_Restore.ipsw)
```
More advanced things you can do is use ``-t`` to save shsh blobs although I'm not sure this works on 64bit. You can also put the device into pwned DFU mode if it's A4 and restore a CFW.

# **Wrap Up**
This tool has saved me many times. I recommend everyone check out idevicerestore if they want a way to restore iOS devices from Linux. If you have an iOS device it's a helpful tool to keep installed even if you won't be using it much.