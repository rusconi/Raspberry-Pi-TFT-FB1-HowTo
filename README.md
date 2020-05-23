## Display framebuffer /dev/fb1 on the TFT.

Works with 2.8" 320*240 ILI9341 TFT

Tested on v1.2 of this display:

![Image of Display](/images/screen.png)

1. Connect the display to the raspberry Pi as below

| Display  |  RPi pin |  GPIO # |
|-|-|-|
| VCC | 1 | 3.3v |
| GND | 6 | gnd |
| CS | 24 | 8 |
| RESET | 13 | 27 |
| DC | 15 | 22 |
| SDI(MOSI) | 19 | 10 |
| SCK | 23 | 11 |
| LED | 33 | 13 |


2. Download and install the tft9341 overlay

SSH into the RPI

```bash
git clone https://github.com/goodtft/LCD-show.git
cd LCD-show/
sudo cp ./usr/tft9341-overlay.dtb /boot/overlays/tft9341.dtbo
```

Update the boot/config.txt file

```bash
sudo nano /boot/config.txt
```

add these lines at the end.

```bash
# turns spi on
dtparam=spi=on
# loads tft module for /dev/fb1
dtoverlay=tft9341, rotate=90
# sets tft backlight pin on
gpio=13=op,dh
```

3. Reboot and test

```bash
sudo reboot
```

When rebooted, SSH in again.

You can then;

* Check that /dev/fb1 exists

    ```bash
    ls /dev/fb1
    ```

* get info about fb1

    ```bash
    fbset -fb /dev/fb1 --info
    ```

* test that the display works.

    ```bash
    cat /dev/urandom > /dev/fb1 
    ```


<div class="text-purple">
  This text is purple, <a href="#" class="text-inherit">including the link</a>
</div>


