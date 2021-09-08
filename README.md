# vscp-python-send-bh1750

Send Illuminance readings in lux from a BH1750 sensor to a VSCP daemon as a [level II illuminance measurement event](https://grodansparadis.github.io/vscp-doc-spec/#/./class2.measurement_str?id=type25).

## Credits

This is work based on work done by **Matt Hawkins**, https://www.raspberrypi-spy.co.uk/?s=bh1750

## Installation and setup

i2c support must be enabled. Use raspi-config to enable i2c.

To verify your hardware you can use i2ctools. Install with

```
sudo apt install i2ctools
```

scan bus with

```
i2cdetect 1
```

you will get something like

```
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- 23 -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- -- 

```

as output.

The _23_ is the address of the BH1750 sensor.

You also need to install smbus support for python. Install with

```
pip3 install smbus
```



## usage

```bash
vscp_send_bh1750.py host user password [guid] [sensorindex] [zone] [subzone]
```

| Parameter | Description |
|----------|-------------|
| **host**     | VSCP host to connect to |
| **user**     | VSCP user to connect as |
| **password** | VSCP password |
| **guid**     | Optional. GUID to use for the sensor. Default to "-", the daemons interface GUID. |
| **sensorindex** | Optional. Index of the sensor to use. Defaults to zero. |
| **zone**     | Optional. Zone to use for the sensor. Default to zero. |
| **subzone**  | Optional. Subzone to use for the sensor. Defaults to zero. |

Typically you would run this script as a cronjob to send data every minute or so.


## example

```
./send_bh1750.py localhost admin secret - 0 0 0
```

Send a reading to a VSCP daemon on the local host using the interface GUID and setting sensorindex, zone and subzone all to zero. This is the same as using

```
./send_bh1750.py localhost admin secret
```

where default values are used for the sensorindex, zone and subzone.

---

This file is part of the [vscp project](https://www.vscp.org)