# Minimalist Computing - Holiday Design Contest

This project is my submission for the Facebook's Minimalist Computing group Holiday Design Contest.

## Design Contest Rules
* Holiday related design
* Can use one 7400-series IC. The logic family does not matter. It can be HC, LS, etc.
* Can use 2 transistors maximum
* Any number of passive components: capacitors, resistors, diodes, coils, LEDs (without any ICs in the LED packages, e.g. self-flashing or color changing LEDs)
* The only external connection is the power supply

## My Design's Description

My design is an eight pointed star with animated LEDs. The shape is inspired by the [Vintage Computing Christmas Challenge 2022](https://logiker.com/Vintage-Computing-Christmas-Challenge-2022).

The [design](KiCad/star-schematic-1.0.pdf) includes:
* A [multivibrator](https://en.wikipedia.org/wiki/Multivibrator), implemented using two transistors - Q1 and Q2, four resistors - R50-R53, and two capacitors - C2 and C3. The multivibrator provides the clock for the rest of the circuit.
  * The choosen values of the R52, R53 - 62 k, C2 and C3 - 2.2 uF result in approximately 5.3 Hz frequency.
  * The formula to calculate the frequency is f = 1 / (ln(2)(R52\*C2+R53\*C3)), or since R52 = R53 and C2 = C3, it can be simplifed to f ~= 0.72/(R52*C2).
* A 4 bit [Johnson counter](https://en.wikipedia.org/wiki/Ring_counter), implemented using a 74*175 - four D-type flip-flops IC.
  * In my own build I used the [74LS175](https://www.ti.com/lit/ds/symlink/sn74ls174.pdf) IC, but I think any other series will work just as well.
* 3 outputs of the counter are connected to the LEDs through current limiting resistors. The last output is not connected to the LEDs. This doubles the delay when all LEDs are on and when all LEDs are off.
  * The LEDs are connected between the inverted outputs of the flip-flops and VCC. This is because TTL/TTL-LS series ICs have the low-level output current I<sub>OL</sub> much higher than the high-level output current I<sub>OH</sub>. For the 74LS175 the values are 16 mA and -800 uA respectively.
  * The current limiting resistors have a fairly large resistance. I used 4.7 k for red LEDs and 10k for green and blue LEDs. This keeps the current well within the IC's I<sub>OL</sub> specifications.

![Star Assembled Board](images/holiday174-star.jpg)

## Design Files

* [Schematic](KiCad/star-schematic-1.0.pdf)
* [PCB Layout](KiCad/star-board-1.0.pdf)

## Bill of Materials

[Holiday174-Star project on Mouser.com](https://www.mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=de9819fc8b) - View and order all components except of the PCB and the power supply. Note, the LEDs are somewhat expensive at Mouser. Use Amazon link in the BoM below - a kit with 250 color LEDs for under $8.

Component type     | Reference | Description                                 | Quantity | Possible sources and notes 
------------------ | --------- | ------------------------------------------- | -------- | --------------------------
PCB                |           | Star PCB - SK103                            | 1        | Buy from my Tindie store: Order from a PCB manufacturer of your choice using provided Gerber or KiCad files
Integrated Circuit | U1        | 74LS175 - Quadruple D-type flip-flop with reset, 16 pin DIP | 1 | Mouser [595-SN74LS175N](https://www.mouser.com/ProductDetail/595-SN74LS175N)
Transistor         | Q1, Q2    | 2N3904                                      | 1        | Mouser [512-2N3904TA](https://www.mouser.com/ProductDetail/512-2N3904TA)
LEDs               | D1 - D49  | 3 mm LEDs                                   | 49       | Amazon [3mm Led Lights, 250Pcs](https://www.amazon.com/dp/B0C5HZ6W99), Mouser [710-151033RS03000](https://www.mouser.com/ProductDetail/710-151033RS03000) - red, [710-151033GS03000](https://www.mouser.com/ProductDetail/710-151033GS03000) - green, [710-151033BS03000](https://www.mouser.com/ProductDetail/710-151033BS03000) - blue. Notes: You can use a variety of colors. Current limiting resistors might need to be adjusted to keep the brightness of the LEDs with different colors roughly the same.
Connector          | J1        | 2 pin header, 2.54 mm pitch, right angle    | 1        | Mouser [649-1012937990202BLF](https://www.mouser.com/ProductDetail/649-1012937990202BLF)
Capacitor          | C1        | 0.1 uF, 50V, MLCC, 5 mm pitch               | 1        | Mouser [810-FG28X7R1H104KNT6](https://www.mouser.com/ProductDetail/810-FG28X7R1H104KNT6)
Capacitor          | C2, C3    | 2.2 uF, MLCC, 5 mm pitch                    | 1        | Mouser [810-FG28X5R1E225KRT6](https://www.mouser.com/ProductDetail/810-FG28X5R1E225KRT6)
Capacitor          | C4        | 47 uF, 10V, Electrolytic, 6.3 mm diameter, 2.5 mm pitch | 1 | Mouser [667-EEA-GA1C470](https://www.mouser.com/ProductDetail/667-EEA-GA1C470)
Resistor           | R1 - R49  | 4.7 kohm - 10 kohm, 0.25 W, axial           | 49        | Mouser [603-CFR-25JB-52-4K7](https://www.mouser.com/ProductDetail/603-CFR-25JB-52-4K7) - 4.7k, Mouser [603-CFR-25JB-52-10K](https://www.mouser.com/ProductDetail/603-CFR-25JB-52-10K) - 10k. Adjust R1-R49 values for the desired LED brightness. It is recommended to use resistors with 4.7k resistance or above. 10k resistors work really nice with blue and bright green LEDs. 4.7k resistors work great with red LEDs
Resistor           | R50, R51  | 4.7 kohm, 0.25 W, axial                     | 2        | Mouser [603-CFR-25JB-52-4K7](https://www.mouser.com/ProductDetail/603-CFR-25JB-52-4K7)
Resistor           | R52, R53  | 62 kohm, 0.25 W, axial                      | 2        | Mouser [603-CFR-25JB-52-62K](https://www.mouser.com/ProductDetail/603-CFR-25JB-52-62K)
Power supply       |           | 5V regulated power supply                   | 1        | USB charger or similar should work. 3 x AA batteries can be used instead

## Licensing

The hardware design, including schematic and PCB layout design files are licensed under the strongly-reciprocal variant of [CERN Open Hardware Licence version 2](license-cern_ohl_s_v2.txt).

