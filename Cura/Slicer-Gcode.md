## Start G-Code

```bash
M220 S100 ;Reset Feedrate
M221 S100 ;Reset Flowrate
;{material_print_temperature} {material_bed_temperature}
M190 S{material_bed_temperature} ;heat bed and wait
G28 ;home XYZ axis
G1 X0 Y0 F2000 ;move to X0 Y0
M109 S{material_print_temperature} T0 ;wait for nozzle to reach temp
;Fix X0 Y0 being outside the bed after homing
G1 Z2.0 F3000 ;Move Z Axis up
G1 X1.3 Y4.8 ;Place the nozzle over the bed
;Code for nozzle cleaning and flow normalization
G92 E0 ;Reset Extruder
G1 Z2.0 F3000 ;Move Z Axis up
G1 X10.4 Y20 Z0.28 F5000.0
G1 X10.4 Y170.0 Z0.28 F1500.0 E15
G1 X10.1 Y170.0 Z0.28 F5000.0
G1 X10.1 Y40 Z0.28 F1500.0 E30
G92 E0 ;Reset Extruder
G1 Z2.0 F3000 ;Move Z Axis up
```

## End G-Code

```bash
G91 ;Relative positioning
G1 E-5 F2700 ;Retract the filament
G1 E-5 Z0.2 F2400 ;Retract and raise Z
G1 X5 Y5 F3000 ;Wipe out
G1 Z10 ;Raise Z more
G90 ;Absolute positionning
G28 X0 Y0 ;Home X and Y
M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed
M84 X Y E ;Disable all steppers but Z
```
