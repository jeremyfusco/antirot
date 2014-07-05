# antirot

Tool to prevent bitrot from creeping onto your long running server(s) hard disks/SSDs.

## Reason this tool exists. 

Through many years of system administration experience, one of the worst scenerios is the long running linux server.
With it's filesystem/disk running for year(s) with no fsck, you are bound to have issues if you restart the machine.

One 'solution' I've always performed when restarting a long running server is to touch /fastboot to prevent files that haven't been read for years and hence possibly triggering bitrot.

This is not ideal. Coming from Netapp/ZFS backed filesystems it feels like the stone age when I have a filesystem without a guaranteed known state. 

Important systems usually have raid. The entire drive is scrubed every week to discover bitrot.

This tool attempts to be an in-between solution. Perhaps you inhereted a new environment with a large number of servers that are long running. Perhaps you have a huge cloud instance and you want to ensure there is no corruption due to improper handling of your virtual drives.

## How antirot performs this function

Antirot will scan your drive and generate manifests for all of your files. Keyed by the modification date you may verify file system integrity by scanning files against the previously generated manifest.

Newer files are ignored, we are primarily concerned with files that have been on the disk for weeks to months as opposed to hours and days.

The simple act of reading a file coerce's a hard drive to verify CRC checksum and sometimes reallocate the sectors, effectively staving off bitrot, and at the very least preventing surprises during your next reboot.


