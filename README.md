# retro-pcbs
This site contains some stuff I have built for old retro computers.

I tinker with electronics, release stuff when I feel like it and I make it public when it's maybe not perfect. I'm not an electronics expert, so I may not always know what I'm doing. I learn the necessary electronics as I use it. Use at your own risk.

Be smart. Don't just trust the stuff I offer for download here. Take a look at schematics and PCB designs beforehand ;-)

Feedback is always very welcome 😄

## WP32 McCake 5.25" bay

This is a 5.25" bay for retro PCs that use the [https://www.serdashop.com/](Serdaco/Serdashop) WP32 McCake [https://github.com/dwhinham/mt32-pi](mt32-pi) waveblaster extension. Be aware that Serdaco offers their own bay. This bay is a DIY alternative with a larger display and a rotary knob for volume control.

Bay + PCB have been tested and seem to work well.

![image](https://user-images.githubusercontent.com/884834/124360159-944fea80-dc28-11eb-87fa-5ab4bda11be3.png)

![image](https://user-images.githubusercontent.com/884834/124390280-16084c80-dceb-11eb-9aac-38e4baddc9fc.png)

![image](https://user-images.githubusercontent.com/884834/124390288-26b8c280-dceb-11eb-93ac-455ed4f14fee.png)

![20210910_171233](https://user-images.githubusercontent.com/884834/132877155-81e0a804-c985-4adc-b823-88f555d96014.jpg)

Gerber: https://github.com/bzeiss/retro-pcbs/blob/main/mccake-5.25-inch-bay/kicad/gerber/mccake-5.25-inch-bay-v1.0.zip

Case STLs: https://github.com/bzeiss/retro-pcbs/tree/main/mccake-5.25-inch-bay/3dmodel

There is no knob for the rotary encoder in the STL directory. I have just grabbed one from thingiverse for it.

### Prerequisites

You need a soldering iron, some solder and a 3D printer to build this. It is very generally easy to build.
The PCB for the front panel can be ordered, for example, from jlcpcb.com, pcbway, oshpark or similar servies.

### BOM

Parts are mostly standard parts and can based obtained easily from AliExpress or any other electronics dealer.

| Quantity | Part                                    | Examples | Comments |
|----------|------                                   | ------ | ------ |
|     1    | Through-hole rotary knob with button    | | |
|     2    | Through-hole standard 4-pin buttons     | | |
|     1    | 2.54mm pin header with 9 pins           | | |
|     1    | 1.3" SH1106 I2C OLED display (not the typical 0.96" one!) | [AliExpress](https://de.aliexpress.com/item/4001244324545.html?spm=a2g0s.9042311.0.0.27424c4dTWHz1p) | Required pin order: VCC-GND-SCL-SDA |
|     1    | IDC cable with at least 9 pins in a row | [Amazon](https://www.amazon.de/dp/B07KFX57HV/ref=cm_sw_em_r_mt_dp_9ASK1YN18FPK2M1SWVQK?_encoding=UTF8&psc=1) | |
|     1    | Serdaco WP32 McCake | | |

### Configuration

These are the changes I have made to my mt32-pi.cfg

```
[system]
usb = off

[audio]
output_device = i2s

[control]
scheme = simple_encoder

[lcd]
type = sh1106_i2c
width = 128
height = 64
```

config.txt:

```
avoid_warnings=2

[pi4]
arm_64bit=1
armstub=armstub8-rpi4.bin
kernel=kernel8-rpi4.img

# Optimized frequency settings for lower energy use/temperature on Pi 4
arm_freq=600
arm_freq_min=100
gpu_freq=100
over_voltage=-16
over_voltage_min=-16
```

The pi4 section should be the default one starting mt32-pi 0.10.0 or so. Make sure you have the arm frequency adjustments in there in order to avoid high temperatures and throttling of the compute module 4.
