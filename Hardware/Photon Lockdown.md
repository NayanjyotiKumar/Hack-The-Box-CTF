![Screenshot 2024-01-09 191515](https://github.com/ValhalaKing16/Hack-The-Box-CTF/assets/94128525/50ae616f-dbae-4312-b44b-ceca8871db5d)# [Photon Lockdown] (https://app.hackthebox.com/challenges/548)

> We’ve located the adversary’s location and must now secure access to their Optical Network Terminal to disable their internet connection. Fortunately, we’ve obtained a copy of the device’s firmware, which is suspected to contain hardcoded credentials. Can you extract the password from it?

As you uzip the file you will see 3 more files :

> ![image](https://github.com/ValhalaKing16/Hack-The-Box-CTF/assets/94128525/3c7ebde0-ec8e-4695-8127-c5c37c4b135b)

So we want to know what files, what’s the nature of these files ,We used the “file” command.

> ![image](https://github.com/ValhalaKing16/Hack-The-Box-CTF/assets/94128525/f9a04941-a60a-4111-9bbd-bb4b9178f6e6)

We knew that the version of the frimware device was 3.0.5.

and hw_ver it’s X1 archive data contains some data i didnt undstood its most probably the firmware name X1.

and the rootfs is a squash file.

So root FS system is a type of file system that contains a compressed version of an operating system.

> Example : This Linux operating system I’m using, I can compress files and directories in a root FS file to create an image that can be used on different devices. This method is particularly useful for embedded systems, such as Internet of Things (IoT) devices, where the size of the operating system is crucial.

So it’s useful if you know how to extract this file.

Squashfs is a compressed read-only file system for Linux. Squashfs compresses files, inodes and directories

so we can use squashfs utility here to be specific unsquashfs which will extract all the content of rootfs file.

So since we created a specific directory to host the contents of the FHIR system, we’re going to create another one called Contents.

> ![image](https://github.com/ValhalaKing16/Hack-The-Box-CTF/assets/94128525/f771e38f-5f22-4d27-88a7-5747f7670def)

> ![image](https://github.com/ValhalaKing16/Hack-The-Box-CTF/assets/94128525/bb179133-d27d-463e-bdd8-9ca37504d3d9)

And as you can see, we have directories, So we have BIN, Dev, etc, Home, Image. These directories are very common in any Linux operating system.

Okay, so this means that rootFS represents a squash image or a compressed file of an entire operating system, Linux operating system.

So our goal here is to find the flag, which is a plaintext password.

So i have decided to utilize one of the Linux Privilege Escalation methods that involves searching for clear-text passwords and dumping credentials.

> grep — include=* .{txt, conf} -rnw ‘/’ -e ‘password’ 2>/dev/null

now this perticular command what this will do is check all file if there is any text, config, php and xml files containg the word HTB if there is any that will print it,

and in the config_default.xml finally found the flag.

![image](https://github.com/ValhalaKing16/Hack-The-Box-CTF/assets/94128525/228c9d22-f013-4af2-bd1c-301cee4b8803)

## Answer
> HTM{N0w_Y0u_C4n_L0gIn}
