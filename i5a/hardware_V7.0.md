Colorlight i5A V7.0 Hardware
===============================


Components
----------

* Lattice ECP5 `LFE5U-25F-6BG256C` ([product page](https://www.latticesemi.com/Products/FPGAandCPLD/ECP5))
* Winbond `25Q32JVSIQ`, 32 Mbits SPI flash ([datasheet](datasheets/w25q32jv_spi_revc_08302016.pdf))
* 2x Broadcom `B50612D` Gigabit Ethernet PHYs ([datasheet](../5a-75b/datasheets/B50610-DS07-RDS.pdf))
* 1x ESMT `M12L64322A` 2M 200MHz SDRAM (organized as 4 x 512k x 32bit) ([datasheet](datasheets/M12L64322A(2S).pdf))
* 10x `74HC245T` Octal Bidirectional Transceiver (used for level translation to 5V)


PCB overview
------------

![PCB front](images/cl-i5a-v70-front.jpg)
![PCB back](images/cl-i5a-v70-back.jpg)


Definitions
-----------


Power
-----
## TODO - these are wrong for the i5a
The maximum voltage at the 5V input is 5.5V, due to the buck converters used.
The 5V rail directly feeds only the FPGA power supplies and the 74HC245T output level shifters.
FPGA power is supplied by 3 buck converters. They are compatible with a TI TLV62565/6 in a SOT23-5 package.

| Buck converter | Vout | Rail | Description               |
|----------------|------|------|---------------------------|
| U34            |1.1V  | Vcc  | Core supply voltage       |
| U37            |1.0V  | Vref | Reference voltage         |
| U38            |3.3V  | Vccio| I/O Driver supply voltage and 3.3V for the rest of the board |


JTAG
----

JTAG is available on a 4-pin header next to the FPGA (U?). VCC/GND are available on a separate 2-pin header.

| Pin | Function |
|-----|----------|
| J9  | TCK      |
| J8  | TMS      |
| J4  | TDI      |
| J1  | TDO      |
|     |          |
| J?  | *3.3V*   |
| J?  | *GND*    |


SPI Flash (U?)
---------------

| Flash Pin | FPGA Pin | Function | Notes |
|-----------|----------|----------|-------|
| 1         | ??       | CS#      |
| 2         | ??       | SO       |
| 3         | _na_     | WP#      | Wired to 3v3
| 4         | _na_     | GND      |
| 5         | ??       | SI       |
| 6         | ??       | SCK      |
| 7         | _na_     | Hold#    | Wired to 3v3
| 8         | _na_     | VCC      | Wired to 3v3



Connections
===========

Clock
-----

# TODO - confirm clock input pin
A 25MHz clock is available at FPGA pin P6, and is also connected to both PHYs.


LED, Button
-----------

# TODO - confirm led/button pins
There is a general purpose, FPGA controlled LED (DATA_LED-) at T6, active low (FPGA pin should be set to open drain).

Additionally, there is a button (R7, KEY+).

PAD N16 -> unpopulated R26


SDRAM U?
---------

The SDRAM is organized as 2Mx32.
# TODO - verify SDRAM pins - at least several will be different

| SDRAM Signal | FPGA Pin for U29 | Notes |
|--------------|------------------|-------|
| DQ0          | B2               |
| DQ1          | A2               |
| DQ2          | C3               |
| DQ3          | A3               |
| DQ4          | B3               |
| DQ5          | A4               |
| DQ6          | B4               |
| DQ7          | A5               |
| DQ8          | E7               |
| DQ9          | C6               |
| DQ10         | D7               |
| DQ11         | D6               |
| DQ12         | E6               |
| DQ13         | D5               |
| DQ14         | C5               |
| DQ15         | E5               |
| DQ16         | A11              |
| DQ17         | B11              |
| DQ18         | B12              |
| DQ19         | A13              |
| DQ20         | B13              |
| DQ21         | A14              |
| DQ22         | B14              |
| DQ23         | D14              |
| DQ24         | D13              |
| DQ25         | E11              |
| DQ26         | C13              |
| DQ27         | D11              |
| DQ28         | C12              |
| DQ29         | E10              |
| DQ30         | C11              |
| DQ31         | D10              |
| BA0          | B7               |
| BA1          | A8               |
| A0           | A9               |
| A1           | B9               |
| A2           | B10              |
| A3           | C10              |
| A4           | D9               |
| A5           | C9               |
| A6           | E9               |
| A7           | D8               |
| A8           | E8               |
| A9           | C7               |
| A10/AP       | B8               |
| DQM0         | _na_             | Wired to GND
| DQM1         | _na_             | Wired to GND
| DQM2         | _na_             | Wired to GND
| DQM3         | _na_             | Wired to GND
| WE#          | B5               |
| CAS#         | A6               |
| RAS#         | B6               |
| CS#          | _na_             | Wired to GND
| NC           | A7               |
| CKE          | _na_             | Wired to 3.3V
| CLK          | C8               |


Gigabit PHYs (U11 & U13)
------------------------

# TODO verify phy pins
PHY0, U3
----------

| U3 Pin  | FPGA Pin | Notes |
|---------|----------|-------|
| GTXCLK  | M2       |
| TXD[0]  | L1       |
| TXD[1]  | L3       |
| TXD[2]  | P2       |
| TXD[3]  | L4       |
| TX\_EN  | M3       |
| RXC     | M1       | Connected to ~RESET via R100
| RXD[0]  | N1       |
| RXD[1]  | M5       |
| RXD[2]  | N5       |
| RXD[3]  | M6       |
| RXD\_DV | N6       |
| MDC     | P3       |
| MDIO    | T2       |
| ~RESET  | P5       | Drives RXC via R100

PHY1, U7
----------

| U7 Pin  | FPGA Pin | Notes |
|---------|----------|-------|
| GTXCLK  | M12      |
| TXD[0]  | T14      |
| TXD[1]  | R12      |
| TXD[2]  | R13      |
| TXD[3]  | R14      |
| TX\_EN  | R15      |
| RXC     | M16      | Connected to ~RESET via R107
| RXD[0]  | P13      |
| RXD[1]  | N13      |
| RXD[2]  | P14      |
| RXD[3]  | M15      |
| RXD\_DV | L15      |
| MDC     | P3       |
| MDIO    | T2       |
| ~RESET  | P5       | Drives RXC via R107


Headers
-------------

It is possible to replace the 74HC245T output drivers with pin-compatible SN74CBT3245A octal fet bus switches to allow for bidirectional I/O. Note that the output drivers are powered from 5V, so the only protection when using 5V I/O are the resistor packs. ECP5 FPGA does not have 5V tolerant I/O.

Connector JP1
---------------
Pin 1 labeled with arrow on top silkscreen layer. Pins are marked alternating, ie. pin 1
is the top-right corner of the connector, pin 2 is bottom-right, pin 49 top-left and pin 50 bottom-left.

| Shared | Buffer      | FPGA Pin | JP600 Pin | JP600 Pin | FPGA Pin | Buffer      | Shared |
|--------|-------------|----------|-----------|-----------|----------|-------------|--------|
| **GND**| **GND**     | **GND**  | **1**     | **2**     | ??       | **XX**      | **XX** |
| **GND**| **GND**     | **GND**  | **3**     | **4**     | ??       | **XX**      | **XX** |
| **GND**| **GND**     | **GND**  | **5**     | **6**     | F15      | U5, chan 0  | JP2.6  |
|        | U6, chan 0  | M7       | **7**     | **8**     | R6       | U6, chan 1  |        |
|        | U6, chan 2  | T6       | **9**     | **10**    | M9       | U6, chan 3  |        |
|        | U6, chan 4  | N7       | **11**    | **12**    | M8       | U6, chan 5  |        |
|        | U6, chan 6  | R2       | **13**    | **14**    | P4       | U6, chan 7  |        |
|        | U2, chan 0  | P7       | **15**    | **16**    | F2       | U2, chan 1  |        |
|        | U2, chan 2  | L5       | **17**    | **18**    | R1       | U2, chan 3  |        |
|        | U2, chan 4  | R7       | **19**    | **20**    | P1       | U2, chan 5  |        |
|        | U2, chan 6  | K5       | **21**    | **22**    | H4       | U2, chan 7  |        |
|        | U3, chan 0  | P8       | **23**    | **24**    | E3       | U3, chan 1  |        |
|        | U3, chan 2  | C2       | **25**    | **26**    | K4       | U3, chan 3  |        |
|        | U3, chan 4  | R8       | **27**    | **28**    | G1       | U3, chan 5  |        |
|        | U3, chan 6  | K3       | **29**    | **30**    | J4       | U3, chan 7  |        |
|        | U4, chan 0  | R5       | **31**    | **32**    | H5       | U4, chan 1  |        |
|        | U4, chan 2  | H3       | **33**    | **34**    | G2       | U4, chan 3  |        |
|        | U4, chan 4  | T4       | **35**    | **36**    | G3       | U4, chan 5  |        |
|        | U4, chan 6  | F1       | **37**    | **38**    | F3       | U4, chan 7  |        |
| JP2.39 | U5, chan 1  | K2       | **39**    | **40**    | J5       | U5, chan 2  | JP2.40 |
| JP2.41 | U5, chan 3  | K1       | **41**    | **42**    | L2       | U5, chan 4  | JP2.42 |
| JP2.43 | U5, chan 5  | J14      | **43**    | **44**    | B16      | U5, chan 6  | JP2.44 |
| JP2.45 | U5, chan 7  | F12      | **45**    | **46**    | **GND**  | **GND**     | **GND**|
| **??** | **??**      | **??**   | **47**    | **48**    | **GND**  | **GND**     | **GND**|
| **??** | **??**      | **??**   | **49**    | **50**    | **GND**  | **GND**     | **GND**|


Connector JP2
--------------
Pin 1 labeled with arrow on top silkscreen layer. Pins are marked alternating, ie. pin 1
is the bottom-left corner of the connector, pin 2 is upper-left, pin 49 bottom_right and pin 50 upper-right.

| Shared | Buffer      | FPGA Pin | JP601 Pin | JP601 Pin | FPGA Pin | Buffer      | Shared |
|--------|-------------|----------|-----------|-----------|----------|-------------|--------|
| **GND**| **GND**     | **GND**  | **1**     | **2**     |          | **5V**      | **5V** |
| **GND**| **GND**     | **GND**  | **3**     | **4**     | ??       | **XX**      | **XX** |
| **GND**| **GND**     | **GND**  | **5**     | **6**     | F15      | U16, chan 0 | JP1.6  |
|        | U20, chan 0 | E14      | **7**     | **8**     | A13      | U20, chan 1 |        |
|        | U20, chan 2 | B14      | **9**     | **10**    | E13      | U20, chan 3 |        |
|        | U20, chan 4 | F14      | **11**    | **12**    | A14      | U20, chan 5 |        |
|        | U20, chan 6 | F16      | **13**    | **14**    | A15      | U20, chan 7 |        |
|        | U19, chan 0 | D16      | **15**    | **16**    | G15      | U19, chan 1 |        |
|        | U19, chan 2 | H14      | **17**    | **18**    | G14      | U19, chan 3 |        |
|        | U19, chan 4 | E15      | **19**    | **20**    | H12      | U19, chan 5 |        |
|        | U19, chan 6 | J13      | **21**    | **22**    | H13      | U19, chan 7 |        |
|        | U18, chan 0 | F13      | **23**    | **24**    | G16      | U18, chan 1 |        |
|        | U18, chan 2 | H15      | **25**    | **26**    | J12      | U18, chan 3 |        |
|        | U18, chan 4 | G12      | **27**    | **28**    | J16      | U18, chan 5 |        |
|        | U18, chan 6 | J15      | **29**    | **30**    | K16      | U18, chan 7 |        |
|        | U17, chan 0 | G13      | **31**    | **32**    | L16      | U17, chan 1 |        |
|        | U17, chan 2 | N12      | **33**    | **34**    | K15      | U17, chan 3 |        |
|        | U17, chan 4 | L13      | **35**    | **36**    | P12      | U17, chan 5 |        |
|        | U17, chan 6 | N11      | **37**    | **38**    | M11      | U17, chan 7 |        |
| JP1.39 | U16, chan 1 | K2       | **39**    | **40**    | J5       | U16, chan 2 | JP1.40 |
| JP1.41 | U16, chan 3 | K1       | **41**    | **42**    | L2       | U16, chan 4 | JP1.42 |
| JP1.43 | U16, chan 5 | J14      | **43**    | **44**    | B16      | U16, chan 6 | JP1.44 |
| JP1.45 | U16, chan 7 | F12      | **45**    | **46**    | **GND**  | **GND**     | **GND**|
| **??** | **??**      | ??       | **47**    | **48**    | **GND**  | **GND**     | **GND**|
| **5V** | **5V**      |          | **49**    | **50**    | **GND**  | **GND**     | **GND**|

Connector J17
-------------

| J17 Pin | FPGA Pin | Notes |
|---------|----------|-------|
| D5V     |          | 5V?   |
| GPIO0   | N14      |       |
| GPIO1   | T13      |       |
| R5      | M14      |       |
| GPIO2   | T15      |       |
| SDA     | P16      |       |
| GPIO3   | L14      |       |
| SCL     | P15      |       |
| GND     |          | GND   |
| CS      | L12      |       |
