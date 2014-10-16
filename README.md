This is a script for syncing files between an Android device and your
computer. I used to just use rsync, but some newer devices (like the
Galaxy Nexus) can't mount as a file system on Mac OS, hence this script.
Instead of using the file system, it uses adb (the Android Debugging
Bridge) to copy files and retrieve metadata (eg: timestamps).

The eventual goal is for this script is to have all of the options rsync
has that I care about (and that are feasible to implement).
Right now the only thing it does is sync from an android device to the
local filesystem. It copies any file that either doesn't exist on the
destination, or where the destination's last-modified time or filesize
are different. It also preserves last-modified times, though note that
for now it is only able to retrieve the last-modified time with 1 minute
resolution.

Syntax is:

python adbsync.py [device]:/path/to/src /path/to/target

where device is the device id as listed by adb devices. This is optional
but allows distinguishing between multiple simultaneously attached devices

TODO list:

- add -v and --progress flags
- add ability to copy a file
- distinguish between copying foo/ and foo (where foo is a directory),
  just like rsync. (The latter creates a foo directory, the former
  copies its contents.)
- add recursive option
- improve timestamp resolution
- preserve other sorts of timestamps?
- add flags to select what to pay attention to: timestamps, sizes, etc.
- test with debugging disabled
- support Android device identifiers
- make it possible to copy from local to Android?
- make it possible to copy Android to Android?
