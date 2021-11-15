# SHT31-D 3D printed radiation shield

Our system uses a simple minimalist design for a 3d printed radiation shield. We provide plans and print settings for a minimalist radiation shield as well as a multi-fin radiation shield found on Thingiverse.  The following includes 3D model STL files used for housing SHT31-D sensors during field deployment, screenshots of two types of radiation shield models, 3D printer settings (for a Prusa I3 MK3S+ in PrusaSlicer software), and photographs of completed radiation shields.

## Tools & Materials
* PRUSA I3 MK3S+ 3D printer, or similar
* PrusaSlicer Software
* PETG filament, we recommend white
* Hot glue gun and glue cartridges or Cyanocoacrylate (CA) glue ("Super glue")

## Minmalist radiation sheild

You can obtain a 3D model of the minimalist shield by downloading [minimalist-shield.stl](../files/minimalist-shield.stl).

<img src=../figs/shieldprint-1.png width=300></img>
<img src=../figs/shieldprint-2.png width=300></img>

Using PRUSA Slicer, or similar software, we recommend the following print settings

| Printer setting | Recommended setting |
|----|---|
|Filament | Generic PETG |
| Nozzle temperature | 235°C |
| Bed temperature | 90°C |
| Layer Height | 0.2 mm (for all) |
| Infill | 25% |
| Support material | Check yes to "Generate support material" and yes to "Support on build plate only" |

Most of these settings are the default values for “0.20mm QUALITY @MK3” in PrusaSlicer software, with only the infill percentage increased and Nozzle/Bed temperatures adjusted to ensure to temperatures fall within range of the recommended temperatures for the brand/type of filament used.

<img src=../figs/shieldprint-3.jpg width=200></img>

## Multi-fin radiation sheild

In the Cannon et al. XXXX study, we testing radiation sheilds using a multi-fin design with 5 or 9 fins. You can obtain the 3D models for the components of the multi-fin shield by downloading [multi-fin-shield.zip](../files/multi-fin-shield.zip).

<img src=../figs/shieldprint-4.png width=400></img><br>
<img src=../figs/shieldprint-5.png width=400></img>

The [multi-fin-shield.zip](../files/multi-fin-shield.zip) file contains the following \*.stl files:

1.  Radiation Shield Vertical Mount (Rad_Shd_Vert_mount_V1.stl)
2.	Radiation Shield Base (Rad_Shd_Base_V1.stl)
3.	Radiation Shield Top (Rad_Shd_Top_V1.stl)
4.  Radiation Shield Fin (Rad_Shd_Fin_V1.stl)
5.	SHT31/iButton Sensor Holder (SHT31_iButton_plugV2.stl)

Use the same settings as the minimalist shield. Some parts such as the Sensor Holder will need support, and others such as the Fins, Base, and Top, will not.

You can print multiple copies of the Radiation Shield Fin to make any sized radiation shield

Once printed, all parts can stacked and glued together (superglue or hot glue).

<img src=../figs/shieldprint-6.jpg width=400></img>
