# ALFN---Alpine-Linux-For-Noobs

Follow up on the arch linux for noob guide. Go check it out or this won't make sense.

Installation hacks:

- setup-alpine
Follow the steps, case sensitive. Use most default first options personally. Create a user as it will allow you to skip: setup-user

apk update
apk upgrade

- setup-xorg-base 
- setup-desktop

Apk search <whatdoyouwant?>

poweroff / reboot

https://wiki.alpinelinux.org/wiki/Desktop_environments_and_Window_managers

---

Coolest part of alpine is that with all the tools for Gnome my install only was only about 3GB.

`Finished! Processed 2926.81 MB in 4.72 seconds (620.26 MB/s)` 

That's it. It's quite cool.

--- 

Struggled a but with the Keyboard locales, they work inside Gnome but not at GDM login screen. 

Also found some priceless code in /etc/gdm/Init:

![wow](https://github.com/user-attachments/assets/149e5dee-ac40-4b87-9dc7-b894194c9b55)

![lol](https://github.com/user-attachments/assets/281a1429-34ce-4104-95e2-c69f34aa5480)

I eventually gave up. Went to sddm on KDE. 

https://blog.floo.fi/changes/installing-alpine-linux-and-kde-plasma

Went to `/usr/share/sddm/scripts/Xsetup` nano into it: setxkbmap "language"

And boom it was finally fixed :)

---

Now as alwyas we want this alpine install to be raid boss mode. 
To do this we are going to do some cool setup idea. 


You see want the Desktop Env, but only sometimes. What I mean is I need terminal access often but not full DE all the time.

`rc-update del sddm default` 

Reboot. Now any time you want the actual de you can `rc-service sddm start` 

`nano ~/.profile` This is your ash home. 
Create an alias `alias start-de="rc-service sddm start"`

Boom now you have the Desktop at hand, just one SHORT command away. 
`start-de` and voilà.

---

Cool set up for qemu:
```
import subprocess
def run_tailvm(image_name):
    # Run the VM
    print(f"Started {image_name}, with {cores} cores and {ram} MB of RAM.")
    command = f"qemu-system-x86_64 -enable-kvm -m {ram} -cpu host -smp {cores} -hda {image_name} -boot c -serial mon:stdio -display none -vnc :0"
```

so we redirect the shell to our shell, set the display to none, but have a VNC ready. 

You can then connect with any VNC client `vncviewer localhost:0` 

Go back to your alias file and add a stop-de with stop instead of start. 


```
Started ./c/myvm4.qcow2, with 8 cores and 8096 MB of RAM.

Welcome to Alpine Linux 3.21
Kernel 6.12.17-0-lts on an x86_64 (/dev/ttyS0)

Welcome to Alpine! Custom scripts by H8D13.
B=> Average Sized <=B
``` 


