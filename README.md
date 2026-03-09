<p align="center">
  <img src="https://github.com/user-attachments/assets/ede24112-1830-45c7-837b-959b381cd149" alt="ICM-42670-P Breakout Board Panel Render" width="90%"/>
</p>

<h1 align="center">ICM-42670-P Motion Sensor Breakout Board</h1>

<p align="center">
  <strong>A compact, breadboard-friendly breakout for the TDK InvenSense ICM-42670-P 6-axis IMU</strong><br/>
  Designed in KiCad 9.0 · Rev v1.0 · By ME! SleepyPandas / Anthony
</p>

<p align="center">
  <a href="https://invensense.tdk.com/wp-content/uploads/2021/07/DS-000451-ICM-42670-P-v1.0.pdf"><img src="https://img.shields.io/badge/Datasheet-ICM--42670--P-0078D4?style=flat-round&logo=bookstack&logoColor=white" alt="Datasheet"/></a>
  <img src="https://img.shields.io/badge/EDA-KiCad%209.0-314CB0?style=flat-round&logo=kicad&logoColor=white" alt="KiCad"/>
  <img src="https://img.shields.io/badge/Layers-2%20Layer%20PCB-orange?style=flat-round" alt="Layers"/>
  <img src="https://img.shields.io/badge/Interface-I2C%20%7C%20SPI%20%7C%20I3C-6A0DAD?style=flat-round" alt="Interface"/>
  <img src="https://img.shields.io/badge/IMU-6--Axis%20%7C%20Accel%20%2B%20Gyro-00897B?style=flat-round" alt="IMU"/>
  <img src="https://img.shields.io/badge/Rev-v1.0-lightgrey?style=flat-round" alt="Rev"/>
</p>

---

## Board Gallery

<table>
  <tr>
    <td align="center" width="70%"><strong>3D Render</strong></td>
    <td align="center" width="30%"><strong>PCB Layout</strong></td>
  </tr>
  <tr>
    <td valign="middle"><img src="https://github.com/user-attachments/assets/c2cd51ff-392e-49f3-959b-0bfe0f817682" alt="3D Render" width="100%"/></td>
    <td valign="middle"><img src="https://github.com/user-attachments/assets/8c48232a-c1b9-4a7c-9a8a-062dbc10d8d4" alt="PCB Layout" width="100%"/></td>
  </tr>
  <tr>
    <td align="center" colspan="2"><strong>Schematic</strong></td>
  </tr>
  <tr>
    <td colspan="2"><img src="https://github.com/user-attachments/assets/ed923745-42ba-4d4a-8860-3aadc7fda16a" alt="Schematic" width="100%"/></td>
  </tr>
</table>

---


## Features

| Feature | Detail |
|:---|:---|
| **IMU** | ICM-42670-P, 6-axis (3-axis accel + 3-axis gyro), LGA-14 package |
| **Power** | On-board **MCP1700-3.3V** LDO regulator (SOT-23), accepts up to 6V input |
| **Interfaces** | I²C (default) & SPI, directly broken out to 0.1″ header pins |
| **Signals** | VCC · GND · CS · INT2 · SCL · SDA · SDO · INT1 · FSYNC |
| **Indicator** | Power LED with 120Ω current-limiting resistor |
| **Form Factor** | Breadboard-friendly with standard 2.54mm pitch headers |

---

## ICM-42670-P Pinout (Official TDK Signal Descriptions)

<img height="437" alt="image" src="https://github.com/user-attachments/assets/5a881535-1700-45d4-b742-afc2b86f5735" />


| Pin | Name | Description |
|:---:|:---|:---|
| 1 | **AP_SDO / AP_AD0** | SPI serial data output (4-wire); I2C slave address LSB |
| 2 | **RESV** | No connect, or connect to GND / VDDIO |
| 3 | **RESV** | No connect, or connect to GND / VDDIO |
| 4 | **INT1 / INT** | Interrupt 1 (push-pull or open drain); all interrupts can map here |
| 5 | **VDDIO** | IO power supply voltage |
| 6 | **GND** | Power supply ground |
| 7 | **FSYNC** | Frame sync input; connect to GND if unused |
| 8 | **VDD** | Power supply voltage |
| 9 | **INT2** | Interrupt 2 (push-pull or open drain) |
| 10 | **RESV** | No connect, or connect to GND / VDDIO |
| 11 | **RESV** | No connect, or connect to GND / VDDIO |
| 12 | **AP_CS** | SPI chip select; connect to VDDIO if using I2C |
| 13 | **AP_SCL / AP_SCLK** | I2C serial clock / SPI serial clock |
| 14 | **AP_SDA / AP_SDIO / AP_SDI** | I2C serial data; SPI data I/O (3-wire) or SPI data input (4-wire) |

---

## Circuit Design Highlights

### Power Regulation
- **MCP1700-3.3V** LDO provides clean, stable 3.3V from a wide input range
- **2.2µF** input & output capacitors (C4, C5) for LDO stability, Microchip's datasheet recommends >= to 1µF but for simplicity we use the same 2.2µF used in other parts of the circuit. 
- Power LED (D1) with **120Ω** series resistor for visual power indication

### Decoupling Strategy

- **C1 (0.1µF)**, High-frequency bypass on VDD, placed closest to IC power pin high-frequency filtering
- **C2 (2.2µF)**, Bulk decoupling on VDD for low-frequency noise filtering
- **C3 (10nF)**, VDDIO Noise Reduction / decoupling from SDA SCL

> [!NOTE] 
> **Layout note:** Decoupling caps are placed as close to the ICM-42670-P power pins as physically possible to minimize parasitic loop inductance (i.e where the trace is the limiting factor for power not the capacitor) Leading to unexpected behavior for sensitive IMUs.

### Interface Configuration
- **CS -> 10kΩ pull-up to VDD**, boots into I²C mode by default
- **SDO/AD0 -> 10kΩ pull-down to GND**, sets I²C address to `0x68`
- **FSYNC -> 10kΩ pull-down to GND**, disables frame sync when not driven

> [!NOTE] 
> **Note:** No I²C pull-ups are included on-board to prevent interfering with SPI.


---

## Bill of Materials

| Ref | Value | Specification | Package / FootPrint | Description | Qty |
|:---:|:---:|:---:|:---:|:---|:---:|
| U1 | ICM-42670-P | - | LGA-14 (2.5x3mm) | 6-axis IMU (accel + gyro) | 1 |
| U2 | MCP1700-330 | 250mA, 178mV dropout | SOT-23 | 3.3V LDO voltage regulator | 1 |
| C1 | 100nF | X7R, ±10%, 16V | 0402 | VDD high-freq bypass | 1 |
| C2, C4, C5 | 2.2µF | X7R, ±10%, 16V | 0402 | VDD bulk / LDO I/O caps | 3 |
| C3 | 10nF | X7R, ±10%, 50V | 0402 | VDDIO bypass | 1 |
| R1, R2 | 10kΩ | ±1%, 50V | 0402 | CS pull-up / AD0 pull-down | 2 |
| R3 | 120Ω | ±1%, 50V | 0402 | LED current limiter | 1 |
| D1 | LED | - | 0603 | Power indicator | 1 |
| J2 | N/A | - | 2.54mm header | 9-pin breakout connector | 1 |

---

## Design Decisions

---

**1. No On-Board I2C Pull-ups**

I2C pull-ups are required since I2C is an open-drain communication protocol, without them the bus lines cannot be pulled HIGH. If pull-ups were included, users running SPI or I3C would have permanent resistive loads on the SDA/SCL lines. In SPI mode this causes unnecessary current draw and can degrade signal integrity by, slowing the rising edge and reducing achievable clock speeds. Leaving pull-ups off the breakout lets the user provide them based on implementation. However I3C is supposedly backwards compatible with I2C so there shouldn't be a major issue the main concern is with SPI.

---

**2. LDO (Low-Dropout Regulator) vs. No Regulator**

The ICM-42670-P officially supports 1.71–3.6V DC directly, so a regulator is not strictly required.But I included the MCP1700-3.3V LDO for two reasons:

1. Most common dev boards (ESP32, Arduino, STM32) operate from 5V USB power rails. The [MCP1700 accepts 2.3-6.0V](https://ww1.microchip.com/downloads/en/DeviceDoc/MCP1700-Data-Sheet-20001826F.pdf) input and regulates it to a clean 3.3V, making this breakout plug-and-play with virtually any platform.
2. The ICM-42670-P contains sensitive MEMS structures (accelerometer and gyroscope masses). Thus it is a much more sensitive IMU to noise. The LDO provides a low-noise, regulated supply, reducing the risk of noise being misinterpreted as motion data or producing unexpected behavior. The MCP1700's 178mV dropout also ensures it stays in regulation even as supply voltage drops.

---

**3. SDO/AD0 Pull-Down**

Usually, SDO / AD0 is pulled down via a 10kΩ resistor to GND, which fixes the I2C/I3C slave address LSB to setting the device address to `0x69`. Which ensures there is no flip flopping between memory addresses for I2C however.

In SPI mode, SDO becomes the MISO line. The 10kΩ pull-down slows the rising edge of the SDO signal. At high SPI clock speeds this can limit achievable data rates and cause some data corruption. Thus it will be user defined.

---

**4. Capacitor Placement and Choice**

Capacitors C1 (100nF) and C2 (2.2µF) are placed as close as physically possible to the ICM-42670-P VDD pin to minimize trace inductance in the power delivery loop. C3 (10nF) decouples VDDIO. Together they filter both high-frequency noise and lower-frequency supply droop, keeping the power rails clean for the MEMS core.

---

**5. Chip Select (CS) Pull-Up**

CS is pulled HIGH via a 10kΩ resistor to VDDIO by default. This ensures the ICM-42670-P boots into I2C/I3C mode rather than SPI mode or leaving it which may cause it to switch beteen SPI and I2C/I3C. Users wishing to use SPI simply drive CS LOW from their microcontroller, the pull-up is easily overridden and does not conflict with normal SPI operation.


---

## Repository Structure

```
ICM-42670-P Breakout Board
├──  ICM-42670-P Breakout Board.kicad_sch    # Schematic source
├──  ICM-42670-P Breakout Board.kicad_pcb    # PCB layout source
├──  ICM-42670-P Breakout Board.kicad_pro    # KiCad project file
├──  production/                              # Fabrication outputs (Gerbers, BOM, positions)
├──  PCB PANEL Production/                    # Panelized PCB for batch manufacturing
├──  Models Photos PDFS/                      # Renders, schematics exports, documentation
└──  README.md
```

---

## Tools Used

- **[KiCad 9.0](https://www.kicad.org/)**, Schematic & PCB layout
- **JLCPCB**, PCBA service
- **OSH Park**, PCB Fabrication (Really cheap 3$ for 3 Boards)
- Shoutout to Altium Designer... Costs an arm and a leg


## 

Designed by me! SleepyPandas

---
