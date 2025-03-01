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

I eventually gave up.
