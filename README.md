Instructions how to mirror Android phone to Linux computer
==========================================================

These instructions will show you how to fully mirror your Android phone
screen to your Linux computer; this means that everything on the phone
will be rendered on the computer, including video playback from any
application, including proprietary player-based applications (like NowTV).

What you need
-------------

- Android phone (Android>5.0);
- Linux computer (tested with Ubuntu 18.04)
- USB cable;

Before you start
----------------

- Make sure that you have installed all the latest updates on your Linux box; on Ubuntu:
```
sudo apt-get update
sudo apt-get upgrade
```
also important is your sytem be a recent version of the OS (example: this method has been tested
succesfully on Ubuntu 18.04LTS but also found impossible to use for 14.04LTS);
- You need to enter the Developer Mode of your Android phone (note: this **does not** mean you
are rooting it!); follow the steps in [this post](https://www.howtogeek.com/129728/how-to-access-the-developer-options-menu-and-enable-usb-debugging-on-android-4.2/); this enables Debugging and USB connection;

Installing needed software packages
-----------------------------------

The only two needed software packages you'll need are:

- `adb` [Android Debug Bridge](http://manpages.ubuntu.com/manpages/cosmic/man1/adb.1.html); [deb](https://ubuntu.pkgs.org/18.04/ubuntu-updates-universe-i386/adb_8.1.0+r23-5~18.04_i386.deb.html); install with `sudo apt-get install adb`
- `scrcpy` - main application - see their [gitHub page](https://github.com/Genymobile/scrcpy);

After you've installed `adb`, install `scrcpy` as a *snap* package; first install `snapd`:

```
sudo apt-get install snapd
```

then install `scrcpy`:

```
sudo snap install scrcpy
```

(see instructions [here](https://snapcraft.io/install/scrcpy/ubuntu)).

Final step: connecting phone and start cast
-------------------------------------------

Once all the software packages have been installed correctly, connect the phone
to the computer via the USB cable and check the `adb` daemon starts:

- with the screen unlocked on the phone, type `adb start-server` (if, for some reason,
the server is running, kill it first by `adb kill-server`);
- the phone will display a sha code and ask you to accept authentication - say yes and
also tick the box saying do not display this message again;
- type `scrcpy` and the application should start immediately!

Do not even try
---------------

Do not even try to install `scrcpy` on older OS's (I tried on Ubuntu 14.04 and tried
both as a *snap* package and build from source) - the problem is that dependency libraries
are old and if the OS is not supported anymore you will have to download and build them
manually one by one. A few issues I encountered:

- install as a *snap* package: `snapd` and `scrcpy` install fine but when running `scrcpy` all fails
since `libmirclient.so.9` is not found (I have `libmirclient.so.7` on Ubuntu 14.04 and updating it to 9
is close to impossible since `mir` needs a whole lot of other dependencies);
- build from source: you will need `python3`; you will also benefit from a virtual environment you can
create using e.g. Anaconda; this is because you will need a host of newer packages and compilers:
  - `gcc > 4.8`
  - `ninja`
  - `meson`
  - `ffmpeg` (note that on Ubuntu 14.04 `ffmpeg` had been temporarily replaced with another package and you'll
need to do a lot of gymnastics to get it installed);

In brief - if you are trying to get it working on an unsupported OS, better not :)
