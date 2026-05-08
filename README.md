<p align="center">
  <img src="https://github.com/user-attachments/assets/ede24112-1830-45c7-837b-959b381cd149" alt="ICM-42670-P Breakout Board Panel Render" width="90%"/>
</p>

<h1 align="center">ICM-42670-P Motion Sensor Breakout Board</h1>

<p align="center">
  <strong>A compact, breadboard-friendly breakout for the TDK InvenSense ICM-42670-P 6-axis IMU</strong><br/>
  Designed in KiCad 10.0 · Rev v1.2 · By ME! SleepyPandas / Anthony
</p>

<p align="center">
  <a href="https://invensense.tdk.com/wp-content/uploads/2021/07/DS-000451-ICM-42670-P-v1.0.pdf"><img src="https://img.shields.io/badge/Datasheet-ICM--42670--P-0078D4?style=flat-round&logo=bookstack&logoColor=white" alt="Datasheet"/></a>
  <img src="https://img.shields.io/badge/EDA-KiCad%2010.0-314CB0?style=flat-round&logo=kicad&logoColor=white" alt="KiCad"/>
  <img src="https://img.shields.io/badge/Layers-2%20Layer%20PCB-orange?style=flat-round" alt="Layers"/>
  <img src="https://img.shields.io/badge/Interface-I2C%20%7C%20SPI%20%7C%20I3C-6A0DAD?style=flat-round" alt="Interface"/>
  <img src="https://img.shields.io/badge/IMU-6--Axis%20%7C%20Accel%20%2B%20Gyro-00897B?style=flat-round" alt="IMU"/>
  <img src="https://img.shields.io/badge/Rev-v1.2-lightgrey?style=flat-round" alt="Rev"/>
</p>

---

## Revision Notes (v1.2)

- Primary project update is now the **0603 parts variant** (easier hand assembly than 0402 passives)
- Passive footprints moved to **0603** across the v1.2 schematic/PCB
- Dedicated v1.2 manufacturing outputs are included in `0603 Parts/production/` (BOM, positions, designators, IPC netlist)
- Project/schematic revision fields updated to **v1.2** in the 0603 KiCad project

---

## Board Gallery

<table>
  <tr>
    <td align="center" width="70%"><strong>3D Render</strong></td>
    <td align="center" width="30%"><strong>PCB Layout</strong></td>
  </tr>
  <tr>
    <td valign="middle"><img src="https://github.com/user-attachments/assets/70ebc165-9789-458b-acc1-ed9eb6a9fbef" alt="3D Render" width="100%"/></td>
    <td valign="middle"><img src="https://github.com/user-attachments/assets/4affdd65-6319-4b5b-a04d-9ff2a4f81e8f" alt="PCB Layout" width="100%"/></td>

  </tr>
  <tr>
    <td align="center" colspan="2"><strong>Schematic</strong></td>
  </tr>
  <tr>
    <td colspan="2"><img src="https://github.com/user-attachments/assets/2c3e6d40-2e6e-4aa9-a850-b450ec5c1d03" alt="Schematic" width="100%"/></td>
  </tr>

  <tr>
    <td align="center" colspan="2"><strong>Prototyping</strong></td>
  </tr>

  <tr>
    <td colspan="2"><img src="https://github.com/user-attachments/assets/7719e367-bad9-4af6-870e-9e31022b1e67" alt="Prototyping" width="100%"/></td>
  </tr>
</table>



---


## Features

| Feature | Detail |
|:---|:---|
| **IMU** | ICM-42670-P, 6-axis (3-axis accel + 3-axis gyro), LGA-14 package |
| **Power** | On-board **MCP1700x** LDO regulator (SOT-23), accepts up to 6V input |
| **Interfaces** | I²C / I3C / SPI, directly broken out to 0.1″ header pins with on-board I²C pull-ups |
| **Signals** | VCC · GND · CS · INT2 · SCL · SDA · SDO · INT1 · FSYNC |
| **Assembly** | v1.2 updates passives to **0603** package sizing |
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
- **MCP1700x** LDO provides a clean regulated rail from a wide input range
- **3.3V rail target** using MCP1700x-330xxTT is maintained at the board's expected low load current
- **2.2µF** input & output capacitors (C4, C5) for LDO stability, Microchip's datasheet recommends >= to 1µF but for simplicity we use the same 2.2µF used in other parts of the circuit. 
- Power LED (D1) with **120Ω** series resistor for visual power indication

### Assembly/Footprint Update (v1.2)

- Passives are standardized to **0603** packages in the v1.2 project for easier hand soldering
- Sensor and regulator footprints remain compact: **LGA-14** (U1) and **SOT-23** (U3)

### Decoupling Strategy

- **C1 (0.1µF)**, High-frequency bypass on VDD, placed closest to IC power pin high-frequency filtering
- **C2 (2.2µF)**, Bulk decoupling on VDD for low-frequency noise filtering
- **C3 (10nF)**, VDDIO Noise Reduction / decoupling from SDA SCL

> [!NOTE] 
> **Layout note:** Decoupling caps are placed as close to the ICM-42670-P power pins as physically possible to minimize parasitic loop inductance (i.e where the trace is the limiting factor for power not the capacitor) Leading to unexpected behavior for sensitive IMUs.

### Interface Configuration
- **SDA -> 10kΩ pull-up to 3V3_Clean** for I²C/I3C bus idle-high behavior
- **SCL -> 10kΩ pull-up to 3V3_Clean** for I²C/I3C clock line idle-high behavior
- **CS -> 10kΩ pull-up to VDDIO**, boots into I²C/I3C mode by default
- **FSYNC -> 10kΩ pull-down to GND**, disables frame sync when not driven
- **SDO/AD0 -> direct breakout (no fixed pull resistor)** for maximum SPI flexibility

> [!NOTE] 
> **Note:** The I²C pull-ups are on SDA/SCL only; this keeps I²C and I3C ready out-of-the-box while avoiding direct loading on SPI MISO paths.


---

## Bill of Materials

| Ref | Value | Specification | Package / FootPrint | Description | Qty |
|:---:|:---:|:---:|:---:|:---|:---:|
| U1 | ICM-42670-P | - | LGA-14 (2.5x3mm) | 6-axis IMU (accel + gyro) | 1 |
| U3 | MCP1700x-330xxTT | 250mA LDO, SOT-23 | SOT-23 | Regulated 3.3V supply rail | 1 |
| C1 | 100nF | X7R, ±10%, 16V | 0603 | VDD high-freq bypass | 1 |
| C2, C4, C5 | 2.2µF | X7R, ±10%, 16V | 0603 | VDD bulk / LDO I/O caps | 3 |
| C3 | 10nF | X7R, ±10%, 50V | 0603 | VDDIO bypass | 1 |
| R1, R2, R4, R5 | 10kΩ | ±1%, 50V | 0603 | CS pull-up / FSYNC pull-down / SDA & SCL pull-ups | 4 |
| R3 | 120Ω | ±1%, 50V | 0603 | LED current limiter | 1 |
| D1 | LED | - | 0603 | Power indicator | 1 |
| J2 | N/A | - | 2.54mm header | 9-pin breakout connector | 1 |

---

## Design Decisions

---

**1. On-Board I2C Pull-ups Added (R4, R5)**

I2C pull-ups are required because I2C uses open-drain signaling and the bus needs passive pull-up resistors to reach logic HIGH. In this revision, dedicated **10kΩ pull-ups were added on SDA and SCL** so the board is immediately usable in I2C and I3C-style wiring. This keeps the breakout more plug-and-play while still preserving speed-focused SPI behavior, since the pull-ups are only on SDA/SCL and not on the SPI data output path.

---

**2. LDO (Low-Dropout Regulator) vs. No Regulator**

The ICM-42670-P officially supports 1.71–3.6V DC directly, so a regulator is not strictly required. But I included an MCP1700x LDO and selected a **3.3V output variant (MCP1700x-330xxTT)** for two reasons:

1. Most common dev boards (ESP32, Arduino, STM32) operate from 5V USB power rails. The [MCP1700 accepts 2.3-6.0V](https://ww1.microchip.com/downloads/en/DeviceDoc/MCP1700-Data-Sheet-20001826F.pdf) input and provides a clean regulated rail, making this breakout plug-and-play with virtually any platform.
2. The ICM-42670-P contains sensitive MEMS structures (accelerometer and gyroscope masses). The LDO provides a low-noise regulated rail, reducing supply-noise-induced measurement error. With expected draw of roughly **0.65mA (IMU) + ~3mA (power LED) ≈ 3.65mA total**, the 3.3V LDO is operating at a very light load and still provides a approximately 3.3V output with a 3.3V input however will not provide the noise reduction benefits at that voltage only 5V.

<p align="center">
  <img width="49%" alt="Load vs Dropout Voltage 5V" src="https://github.com/user-attachments/assets/302a4a32-f03d-4c58-ad68-5d00fbecf10c" />

  <img width="49%" alt="Load vs Dropout Voltage 2.8V" src="https://github.com/user-attachments/assets/88e85129-4c84-4228-a25e-46bbcff06a3f" />
</p>

---

**3. SDO/AD0 Configuration for Speed Flexibility**

In this revision, **SDO/AD0 is left without a fixed pull resistor** so the line can be defined by the host design. For I2C/I3C use, address selection can still be handled externally as needed.

In SPI mode, SDO becomes the MISO line. Avoiding a permanent pull resistor helps preserve edge rate and signal integrity at higher SPI clock speeds.

---

**4. Capacitor Placement and Choice**

Capacitors C1 (100nF) and C2 (2.2µF) are placed as close as physically possible to the ICM-42670-P VDD pin to minimize trace inductance in the power delivery loop. C3 (10nF) decouples VDDIO. Together they filter both high-frequency noise and lower-frequency supply droop, keeping the power rails clean for the MEMS core.

---

**5. Chip Select (CS) Pull-Up**

CS is pulled HIGH via a 10kΩ resistor to VDDIO by default. This ensures the ICM-42670-P boots into I2C/I3C mode rather than entering an undefined mode at startup. Users wishing to use SPI simply drive CS LOW from the microcontroller; the pull-up is weak enough to be overridden during normal SPI operation.


---

## Repository Structure

```
ICM-42670-P Breakout Board
├──  Draw.kicad_wks                            # Custom KiCad worksheet
├──  PersonalNotes.md                          # Project notes
├──  Models Photos PDFS/                       # Renders, schematics exports, documentation
├──  production/                               # Top-level fabrication outputs
│   ├── bom.csv
│   ├── designators.csv
│   ├── netlist.ipc
│   ├── positions.csv
│   └── backups/
├──  Schematic PCB Design/                     # Active v1.2 (0603) design files
│   ├── ICM-42670-P Breakout Board 0603.kicad_sch
│   ├── ICM-42670-P Breakout Board 0603.kicad_pcb
│   ├── ICM-42670-P Breakout Board 0603.kicad_pro
│   ├── ICM-42670-P Breakout Board 0603.csv
│   ├── production/                            # v1.2 fabrication outputs
│   │   ├── bom.csv
│   │   ├── designators.csv
│   │   ├── netlist.ipc
│   │   ├── positions.csv
│   │   └── backups/
│   └── ICM-42670-P Breakout Board 0603-backups/
├──  V1 Old 0402 Design/                       # Legacy 0402 design archive
│   ├── ICM-42670-P Breakout Board.kicad_sch
│   ├── ICM-42670-P Breakout Board.kicad_pcb
│   ├── ICM-42670-P Breakout Board.kicad_pro
│   └── PCB PANEL Production/                  # Panelized legacy production design
├──  ICM-42670-P Breakout Board-backups/
└──  README.md
```

---

## Tools Used

- **[KiCad 10.0](https://www.kicad.org/)**, Schematic & PCB layout
- **JLCPCB**, PCBA service
- **OSH Park**, PCB Fabrication (Really cheap 3$ for 3 Boards)
- Shoutout to Altium Designer... Costs an arm and a leg


## 

Designed by me! SleepyPandas

---
