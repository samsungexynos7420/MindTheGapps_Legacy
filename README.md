# MindTheGapps package fix up
Normally if you have Lineage recovery or a supported device, flashing the recommended Gapps package, MindTheGapps, is easy as flashing or sideloading the zip file. However, if we use TWRP on a legacy device, we run into problems.

Normally you will encounter this error:
> Could not mount /mnt/system! Aborting <BR>
> Updater process ended with ERROR: 1

This prevents us from installing the package. This is because in the install script, it fails to get the /system mount and instead gets a different mount, something like /usbstorage or something instead.

There is a simple fix for this however.

# Step by step guide on how to fix this yourself
1. Download the correct MindTheGapps for your device
2. Extract the Gapps package into a folder and open it
3. Navigate to META-INF/com/google/android and open update-binary in a text editor
4. Find the get_block_for_mount_point() function and replace the contents with
   ```
   cat /etc/recovery.fstab | cut -d '#' -f 1 | grep /system | grep -o '/dev/[^ ]*' | head -1
   
5. Save and re-compress as a zip file
6. Flash the modded package and it should work

This repo is here to document this process, and to also provide already modded packages for those who either don't want to do this, or you just cannot do it for whatever reason. 

# Downloads
[Android 13 ARM64]: https://github.com/samsungexynos7420/MindTheGapps_Legacy/releases/download/13arm64-20231025_200931/MindTheGapps_Legacy-13.0.0-arm64-20231025_200931.zip "MindTheGapps_Legacy-13.0.0-arm64-20231025_200931.zip" 
[Android 13 ARM64]
