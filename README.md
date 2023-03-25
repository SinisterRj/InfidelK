# Inline Filament Diameter Estimator, Lowcost (InFiDEL) for Klipper

WARNING: Work in development!

![InFiDEL K 3d view](https://github.com/SinisterRj/InfidelK/blob/main/Images/Infidelk.png)

This is a low cost filament sensor based on:

https://github.com/drspangle/infidel-sensor

https://www.thingiverse.com/thing:4138933

For configuration, calibration procedure and use, please check: https://www.klipper3d.org/Hall_Filament_Width_Sensor.html

You will need 2 analogic inputs on your main board to use the sensors. If you don't have these analog inputs available, one option is to use an arduino uno/nano as a secondary MCU on klipper and use its I/O ports. To flash the arduino, follow these instructions: https://www.youtube.com/watch?v=-tm3PYYyXOY&t=237s or flash the pre-compiled firmware from here (atmega 328p CPUs only).

## Bill of Materials (BOM):

### Hardware:
2x 623 bearings (preferably 623-2Z / 623-ZZ);\
1x 5x1,5mm N35 magnet;\
2x 5x8mm pin (you can cut from 5mm drill rod);\
1x 3x21mm shaft (you can cut from 3mm drill rod);\
1x M5 grub screw;\
1x 4mm OD spring (from automatic pen).
Short length of PTFE tube

### Electronics:
2x ss49e hall sensors

### Tools for calibration:
1x 2mm drill bit;\
1x 1.75 mm drill bit;\
1x 1.5 mm drill bit;\
1x Caliper or micrometer.

### Extra:
2x M3x4mm (5mm OD) brass heat insert

## Klipper configuration

You can find an updated hall sensor module of klipper in klipper´s folder ot this github repo. Just download it and overwrite the original one at: `~/klipper/klippy/extras` on your klipper installation.

This new module has new features:
1) 3 point calibration;
2) multiple sensor.

To configure your printer.cfg, you should give the sensor a name and define 3 points of calibration, like in the example bellow:
```
[hall_filament_width_sensor sensor_1]
adc1: PC0
adc2: PC1

cal_dia1: 1.49
cal_dia2: 1.75
cal_dia3: 1.965

raw_dia1: 12007
raw_dia2: 11593
raw_dia3: 11082

default_nominal_filament_diameter: 1.75

measurement_delay: 10
measurement_interval: 1
logging: True
```

And also, you must specify the sensor name for all the GCODEs now, like the these examples:

`
QUERY_FILAMENT_WIDTH SENSOR=sensor_1
`\
`
QUERY_RAW_FILAMENT_WIDTH SENSOR=sensor_1
`\
`
RESET_FILAMENT_WIDTH_SENSOR SENSOR=sensor_1
`
