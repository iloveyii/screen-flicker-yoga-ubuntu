# Screen flicker in Yoga 910 using Ubuntu

The screen start flickering as soon as you install and start OS.


## 1 - Solution 

I first followed the following :


- Edit /etc/default/grub

Add i915.enable_rc6=0 GRUB_CMDLINE_LINUX_DEFAULT
Run sudo update-grub
Reboot (optional)
Create and edit ~/.drirc:

```
<device screen="0" driver="dri2">
    <application name="Default">
    <option name="vblank_mode" value="0"/>
    </application>
 </device>
 ``` 
- Create and edit /usr/share/X11/xorg.conf.d/20-intel.conf:

``` 
  Section "Device"
    Identifier "Intel Graphics"
    Driver     "intel"
    Option     "AccelMethod" "uxa"
    Option     "TearFree" "true"
    Option     "DRI" "3"
  EndSection
``` 
- Reboot

### But the above did not work


## 2- Solution - worked
- Press escape as soon as Ubuntu starts to goto startup menu
- Choose Ubuntu Advanced Options and press enter
- Choose the kernel at top and press `e`
- Find the line that starts with `linux` , and add the following at the end of that line:
  `i915.enable_rc6=0`
- Press F10 (with Fn key)
- I had two kernels and only it worked with `rinux-image-5.4.0-51-generic (recovery)` 


### Useful commands
- See a list of intalled kernels
`dpkg --get-selections | grep linux-image`
- See the running kernel
`uname --all`
- This gives some customization `sudo apt install grub-customizer`


## 3 - Upgrade kernel to latest
   - `sudo apt-add-repository -y ppa:cappelikan/ppa`
   - `sudo apt update`
   - `sudo apt install mainline`
   - Launch mainline and install the version from the list
   
### Set default kernel version
   - Find grub location `export GRUB_CONFIG='sudo find /boot -name "grub.cfg" '`
   - `sudo grep 'menuentry ' $GRUB_CONFIG | cut -f 2 -d "'" | nl -v 0`
   - `sudo nano /etc/default/grub` and set `GRUB_DEFAULT=1`
   - `sudo update-grub`
   - Reboot and repeat step 2 above to remove flicker




## Links
- https://gist.github.com/timsueberkrueb/bc17e40d1a88671b66d074ba3b47fbe2