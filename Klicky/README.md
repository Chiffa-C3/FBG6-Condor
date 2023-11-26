# Настройка Klicky

Файлы из папки Config скопировать рядом с файлом конфигурации прошивки Klipper `config.cfg`

Заходим в сам файл config.cfg и добавляем в начало 

```
[include klicky-variables.cfg]
[include klicky-macros.cfg]
[include klicky-bed-mesh-calibrate.cfg]
[include klicky-screws-tilt-calculate.cfg]
```

Добавляем в любом месте файла эти блоки настроек

```
[probe]
pin: ^PC4
x_offset: 2.5
y_offset: 30
z_offset: 3.8 # расстояние от кончика сопла до концевика, подбирается калибровкой через скрипт PROBE_CALIBRATE
speed: 5.0
samples: 3
sample_retract_dist: 5.0
samples_result: average
samples_tolerance: 0.1

[bed_mesh]
speed: 60
horizontal_move_z: 5
mesh_min: 7.5, 35
mesh_max: 240, 200
probe_count: 6,4
mesh_pps: 2, 2
algorithm: bicubic
fade_start: 1
fade_end: 10

[screws_tilt_adjust]                     
screw1: 25, 145
screw1_name: back left screw
screw2: 225, 145
screw2_name: back right screw
screw3: 225, 1
screw3_name: front right screw
screw4: 25, 1
screw4_name: front left screw
speed: 200
screw_thread: CW-M4
horizontal_move_z: 10
```

Находим конфигурационный блок под названием `[stepper_z]` и в нем ищем строку `endstop_pin`, комментируем ее знаком # и вставляем ниже `endstop_pin: probe:z_virtual_endstop` чтобы получилось как на примере ниже:
```
#endstop_pin: !PC8
endstop_pin: probe:z_virtual_endstop
```

Для датчика Klicky используется пин PC4 и земля.
<img src=".Klicky/PIC/plate.png" alt="plate" style="zoom:30%;" />