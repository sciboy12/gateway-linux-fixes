# gateway-linux-fixes
Various fixes for newer (Gemini Lake-based) Gateway laptops on Linux

Tested on a 2020 Gateway Flip 11 (GWTC116-2), using Arch Linux and Xfce4.

## Audio

* Install at Linux 5.17 or newer

* Force a specific ALSA card order:

```
echo "options snd-hda-intel index=0
options snd-usb-audio index=1" | sudo tee /etc/modprobe.d/snd-card-order.conf
```

* Increase the Headphone volume (applies to the internal speakers as well, for some reason):

```
amixer -c 1 set 'Headphone',0 3
```

* Disable powersave on the sound chip to fix popping sound:

```
echo "options snd-hda-intel power_save=0" | sudo tee /etc/modprobe.d/snd-hda-intel.conf
```
* If using TLP, disable `SOUND_POWER_SAVE_ON_AC` and `SOUND_POWER_SAVE_ON_BAT`

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
