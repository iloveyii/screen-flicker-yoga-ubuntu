# Screen flicker in Yoga 910 using Ubuntu

The screen start flickering as soon as you install and start OS.


## Solution 

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


## Solution - worked
- Press escape as soon as Ubuntu starts to goto startup menu
- Choose Ubuntu Advanced Options and press enter
- Choose the kernel at top and press `e`
- Find the line that starts with `linux` , and add the following at the end of that line:
  `i915.enable_rc6=0`
- Press F10 (with Fn key)










## Links
- https://gist.github.com/timsueberkrueb/bc17e40d1a88671b66d074ba3b47fbe2