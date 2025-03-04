# ALFN---Alpine-Linux-For-Noobs

Follow up on the arch linux for noob guide. Go check it out or this won't make sense.

## Installation hacks:

- setup-alpine
Follow the steps, case sensitive. Use most default first options personally. Create a user as it will allow you to skip: setup-user

apk update
apk upgrade

- setup-xorg-base 
- setup-desktop

apk search <whatdoyouwant?>
apk add/del 

(apk add linux-utils) 

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

I eventually gave up. Went to sddm on KDE, always reliable. 

https://blog.floo.fi/changes/installing-alpine-linux-and-kde-plasma

Went to `/usr/share/sddm/scripts/Xsetup` nano into it and add: `setxkbmap "language"` 

For example: `setxkbmap "fr"

And boom it was finally fixed :) Thanks to the link above!

---

Now as alwyas we want this alpine install to be raid boss mode. 
To do this we are going to do some cool setup idea. 

You see want the Desktop Env, but only sometimes. What I mean is I need terminal access often but not full DE all the time.

`rc-update del sddm default` 

Reboot. Now any time you want the actual de you can `rc-service sddm start` 

`nano ~/.profile` This is your ash home. 
Create an alias `alias start-de="rc-service sddm start"`
`source ~/.profile` to apply changes.

Boom now you have the Desktop at hand, just one SHORT command away. 
`start-de` and voilà.

Don't forget to `chmod +x <script.sh>` 

Couple of other things to customize: 
`/etc/profile.d` Any script in here that is executable will run automatically at login. 

apk add fastfetch
Create a simple script ff.sh:

```
#!/bin/sh

fastfetch
sleep 5
clear
```

Now you will have the nice fast fetch logo everytime you log-in. 
The first line is a shebang, it basically is an identifier for what to use to run the script. 

The same could be applied to a Python script using: `#!/bin/python` 

Understand the core file system:
The `~` means home directory (if you are root it will be empty, that's normal) 
You can cd `/` then `ls` to start seeing all the system files. 

If you are a user (provided you created one) then you will see Desktop, Documents, etc 

If you go to /bin you can find all the possibilites. In this case python is not in the root /bin but in the /usr/bin. So we will change the shebang to `#!/usr/bin/python` you can use `which python` to find out. 

Don't forget to `source ~/.profile` everytime you make add an alias.

Example:

![ex](https://github.com/user-attachments/assets/6dfd515b-44f8-453f-8170-0e8309de9250)

_You can see also that you can create scripts on the user and easily link them system wide this way_

My launch script (ff.sh):


---

## Qemu setup:

Insanely raidboss mode. 

```
import subprocess
def run_tailvm(image_name):
    # Run the VM
    print(f"Started {image_name}, with {cores} cores and {ram} MB of RAM.")
    command = f"qemu-system-x86_64 -enable-kvm -m {ram} -cpu host -smp {cores} -hda {image_name} -boot c -serial mon:stdio -display none -vnc :0"
```

So we redirect the shell to our host shell, set the display to none, but have a VNC ready. 

You can then connect with any VNC client `vncviewer localhost:0` 

Go back to your alias file and add a stop-de with stop instead of start. 

This allows for a kind of dual set-up but just when needed in terms of ressources ? 

![Dual](https://github.com/user-attachments/assets/ea1dcad5-0cbb-4060-ad5e-35c0326c59a1)

Fòr example you can also kill a process from shell when frozen in DE. 

```
pgrep problem
kill ID

More useful stuff

apk add xkill (another one for frozen stuff lets you just click it to kill) 

Kernel logs
tail -f /var/log/messages
dmesg -w

Services
rc-service <service_name> status
```




