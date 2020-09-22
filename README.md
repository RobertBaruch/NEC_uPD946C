# NEC_uPD946C

![Die image](https://raw.githubusercontent.com/RobertBaruch/NEC_uPD946C/master/thumb.jpg)

Die images of the NEC uPD946C calculator chip, presumed to be from 1982.

These were taken with a metallurgical microscope with a motorized X-Y stage. The die was very close to level, but might not be exactly level. The camera's lens might not be perfectly non-distorting.

You can download the images [here](https://drive.google.com/drive/folders/1EZuC4RS0huGkSnrBKzJFUDfczR2DHr1X?usp=sharing). This contains:

* `top` (directory): images of the chip with its metal and glass layer intact.
* `bottom` (directory): images of the chip with metal and glass layer removed by hydrofluoric acid.
* `top.zip`: top images in a zip file (281 MB).
* `bottom.zip`: bottom images in a zip file (189 MB).
* `sample_top_stitch.jpg`: Stitch of top images by Microsoft's Image Composite Editor (114 MB).
* `sample_bottom_stitch.jpg`: Stitch of bottom images by Microsoft's Image Composite Editor (68 MB).

You can use these images to develop stitching algorithms, or test your stitching algorithm. Or, you can reverse engineer the calculator chip!


## Technology

![Chip marking](https://raw.githubusercontent.com/RobertBaruch/NEC_uPD946C/master/chip_marking.jpg)

The chip consists solely of PMOS. The feature size appears to be 2.5um. Gates seem to be measured in increments of this amount.

Voltage supplies to this chip are 0v (VSS), -5v (VDD), and -10v (VGG).

The chip contains an oscillator with an internal resistor. The timing of the oscillator is set when paired with the external capacitor.

## External circuit

![Monroe 98 calculator](https://raw.githubusercontent.com/RobertBaruch/NEC_uPD946C/master/monroe98.jpg)

According to [MyCalcDB](http://mycalcdb.free.fr), the uPD946C chip was used in various calculators:
* [BMB 80MF](http://mycalcdb.free.fr/main.php?l=0&id=123)
* [Canon Palmtronic 8](http://mycalcdb.free.fr/main.php?l=0&id=248) (some models)
* [Brother 518E](http://mycalcdb.free.fr/main.php?l=0&id=190)
* [Panasonic 8501](https://vintage-technology.club/pages/calculators/p/panasonic8501.htm)
* and many more.

My uPD946C calculator chip was removed from a Monroe model 98 handheld calculator. For the schematic of this calculator, see [`monroe98_schematic.pdf`](https://raw.githubusercontent.com/RobertBaruch/NEC_uPD946C/master/monroe98_schematic.pdf).

The display is a 9-digit vacuum fluorescent display manufactured by Futaba. Each digit has the usual 7 segments, plus a decimal point.

![Vacuum fluorescent display](https://raw.githubusercontent.com/RobertBaruch/NEC_uPD946C/master/vfd.jpg)

The power supply is a blocking oscillator with additional stuff. It generates the voltages for the chip (VDD, VGG) plus the VFD cathode/filament voltage of 3.5 VAC and VFD anode/grid voltage of -28v (VLL).

The keyboard matrix is as follows:

|      | K4 | K5 | K6
|------|----|----|----
| SEGA | =  |SQRT| 1
| SEGB | M+ | RM | 2
| SEGC | M- | CM | 3
| SEGD | +  | (pi)   | 4
| SEGE | -  | +/-| 5
| SEGF | DIV| 1/x| 6
| SEGG | x  |x<sup>2</sup> | 7
| K8   | .  |    | 8
| SEGP | CE |    | 9
| VSS  | %  | C  | 0


The two missing elements in the keyboard matrix may or may not have a function. SEGD/K5 is presumed to be pi, because of the way the BMB 80MF calculator is designed (see below).

Interestingly, one of the matrix rows is fixed to VSS.

The keyboard also has a switch which switches VSS.

## Pinout

| Pin  | Description 
|-----:|-------------
| 1    | VSS/EXT_C (external timing capacitor for clock)
| 2    | DIG9 (rightmost digit enable)
| 3    | DIG8
| 4    | DIG7
| 5    | DIG6
| 6    | DIG5
| 7    | DIG4
| 8    | DIG3
| 9    | DIG2
| 10   | DIG1 (leftmost digit enable)
| 11   | K6 (keyboard column)
| 12   | K5 (keyboard column)
| 13   | K4 (keyboard column)
| 14   | VSS (0v)
| 15   | N/C (was measured at -5.8v)
| 16   | SEGP/K (segment decimal point, keyboard row)
| 17   | K8 (keyboard row)
| 18   | SEGG/K (segment G, keyboard row)
| 19   | SEGF/K (segment F, keyboard row)
| 20   | SEGE/K (segment E, keyboard row)
| 21   | SEGD/K (segment D, keyboard row)
| 22   | SEGC/K (segment C, keyboard row)
| 23   | SEGB/K (segment B, keyboard row)
| 24   | SEGA/K (segment A, keyboard row)
| 25   | VGG (-10v)
| 26   | VDD (-5v)
| 27   | VGG (-10v)
| 28   | EXT_C (external timing capacitor for clock)


Pin 15 may or may not have a function.

## Pi

The [BMB 80MF calculator](http://mycalcdb.free.fr/main.php?l=0&id=123) is based around the same uPD946C chip. It has an F key for function, and F-TIMES is x<sup>2</sup>, F-DIV is 1/x, F-MINUS is +/-, F-EQUALS is SQRT, and F-PLUS is pi. This implies that the uPD946C has pi available as a constant, but is simply not accessible in the Monroe 98 calculator without modifying the keyboard matrix.

I found it interesting that some functions are accessed via two keypresses: the F key and another key. Since these correspond exactly with the K5 kyboard column in the Monroe 98, I presume that one of the missing functions, SEGD/K5, is pi.