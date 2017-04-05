# One must kill the Asus TF700T in order to save it
I bought an Asus Transformer Infinity back in 2013 to take notes on PowerPoint slides. It worked well at first, until I installed the OTA upgrade to Android 4.2. Then it became clear that the only "infinite" part of it was the lag that would occur under even tiny amounts of IO.  Such as loading a webpage, which is mainly what a tablet is supposed to do?  So it sat in a shoe box for the past two years.  Supposedly installing a different ROM fixes the issue for some folks.  It did for me.  Here's the newbie guide:

1. You need to unlock the bootloader.  [But first, you'll need to remove your Google account from the tablet.](http://www.transformerforums.com/forum/transformer-pad-300-development/45021-password-needed-unlock-3.html) The unlock tool wants your password, and it uses some old, unsupported Google auth API.  It will acquiesce if it can't find any accounts.
2. Download the unlock tool for bootloader from [one](http://thedroidlawyer.com/2014/08/improve-asus-transformer-infinity-pad-tf700t/) of a number sketchy [websites](https://www.asus.com/us/Tablets/The_New_ASUS_Transformer_PadTF701T/HelpDesk_Download/).  Version 8 worked for me.  Other versions gave me "invalid group signature errors." YMMV.
3. Enable developer mode, plug the tablet into a computer and install the unlocker app with `adb install.` Run it and unlock the bootloader.
4. Install [TWRP](https://twrp.me/devices/asustransformerinfinityTF700T.html) with `fastboot`.
5. Boot into TWRP using the recovery mode (power + volume down). Format cache with ext4.  Format /data with f2fs.
6. `adb push` your desired ROM onto the device over USB. I used Timduru's [Katkiss ROM](http://public.timduru.org/Android/KatKiss/6.0/) and it works nicely.  (ROM is a misnomer, since it's getting written onto SSD..?)
7. Install ("flash") a new ROM using the option in TWRP. 
8. Push and flash [SuperSU](http://www.supersu.com/download).
9. Push and flash [gapps](http://opengapps.org/).
10. Cross your fingers and hit reboot.  If all went accounting to plan, you'll boot into a shiny, new, usable OS.
