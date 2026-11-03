# micro_bec

A small step-down BEC, copied  matek micro BEC 6-30V as best I could

- Input: 6-30V (2-6S)
- Output: 5V by default, 9V with JP1 bridged (9V needs 3S or more)
- Current: 1.5A continuous, 2.5A peak
- Size: about 14 x 10mm, one 4-pin 2.54mm header

## Circuit

TI LMR51430YFDDCR synchronous buck (4.5-36V in, 3A, 1.1MHz, forced PWM), TSOT-23-6.

| Part          | Value                                           |
| ------------- | ----------------------------------------------- |
| Input caps    | 2x 4.7uF 50V                                    |
| Bootstrap cap | 100nF, CB to SW                                 |
| Inductor      | 4.7uH, Isat 4.5A                                |
| Output caps   | 2x 22uF 25V 0805                                |
| Feedback      | 100k top, 13.7k bottom, 15k + JP1 to GND for 9V |

Output voltage is `0.6V x (1 + 100k / R)`:

- JP1 open: R = 13.7k, ~4.98V
- JP1 bridged: R = 13.7k || 15k, ~8.98V

## Pinout

| Pin            | Net  |
| -------------- | ---- |
| 1 (square pad) | VIN  |
| 2              | GND  |
| 3              | GND  |
| 4              | VOUT |

## Libraries

The inductor footprint is in `libs.pretty`, pulled from LCSC with `easyeda2kicad`.
Add it as a footprint library named `mp2315` with path `${KIPRJMOD}/libs.pretty`
(Preferences > Manage Footprint Libraries > Project Specific Libraries).

