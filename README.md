# gateway-linux-fixes
Various fixes for newer (Gemini Lake-based) Gateway laptops on Linux

Tested on a Gateway Flip 11 (GWTC116-2), using Arch Linux and XFCE4.

## Audio

* Install at Linux 5.17 or newer

* Force a specific ALSA card order:

```
options snd-hda-intel index=0
options snd-usb-audio index=1
```

* Increase the "Headphone" volume (applies to speakers as well):

```
amixer -c 1 set 'Headphone',0 3
```

* Disable powersave on the sound chip to fix popping sound:

```
echo "options snd-hda-intel power_save=0" | sudo tee /etc/modprobe.d/snd-hda-intel.conf
```
## WiFi

This process needs to be repeated for all kernel updates:

```
git clone git://github.com/lwfinger/rtl8723du.git -b v5.13.4
cd rtl8723du
make -j$(nproc)
sudo make install
```

## Touchscreen

WIP
