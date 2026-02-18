# Variscite DART-MX9x Development Fixture
**Production Test and Validation Tool for DART-MX91/93/95 Motherboards**

![DART Test Fixture - ISO View](docs/images/3d-render.png)

---

## Overview

Professional test fixture designed to validate motherboard designs before installing expensive Variscite DART System-on-Modules. This tool is used in production testing to verify power delivery, signal routing, and connector integrity on custom carrier boards.

**Compatible with:**
- Variscite DART-MX91
- Variscite DART-MX93
- Variscite DART-MX95

**Note:** This fixture matches the MX9x form factor and is **not compatible** with DART-6UL modules (different connector pinout).

---

## The Problem

When developing custom carrier boards for Variscite DART modules:

**Without a test fixture:**
- Must install expensive SoM ($100-300+) to test basic motherboard functionality
- Risk damaging SoM if power supply has issues
- Cannot validate power delivery under load without live module
- Difficult to troubleshoot signal routing without functional hardware
- Time-consuming to verify each production board before SoM installation

**This fixture solves all of these issues** by providing a low-cost, reusable validation tool.

---

## Key Features

### 1. Visual Power Validation
Four LED indicators verify proper power delivery to DART module connector:

- **VBAT LED:** Main 3.3V power rail (required for all modules)
- **USB1_VBUS LED:** 5V power for USB1 domain
- **USB2_VBUS LED:** 5V power for USB2 domain  
- **VCC_MX95 LED:** Additional 3.3V rail (DART-MX95 only)

**Instant visual confirmation** that power is reaching the correct pins before installing the SoM.

### 2. Power Supply Load Testing
Dedicated test loops connected to 3.3V and GND enable:
- Electronic load connection for power supply validation
- Verification that regulators can deliver required current
- Stability testing under realistic load conditions
- Voltage drop and ripple measurements

**Validates power supply performance** without risking damage to expensive modules.

### 3. Signal Breakout Headers
Optional 0.1" header positions for critical signals:

| Signal | Description | Pins |
|--------|-------------|------|
| **USB1** | USB1 data lines | D+, D-, GND |
| **USB2** | USB2 data lines | D+, D-, GND |
| **I2C1** | I2C bus 1 | SDA, SCL, GND |
| **UART1** | Serial console | TX, RX, GND |

**Use as test points or populate headers** for deeper signal integrity troubleshooting.

---

## Use Cases

### Production Testing (Primary Use)
**Every production motherboard is validated using this fixture before SoM installation:**

1. Install test fixture in DART connector
2. Power up motherboard
3. **Visual check:** Verify all required LEDs illuminate
4. **Power validation:** Connect electronic load to test loops, verify regulation under load
5. **Signal verification (if needed):** Probe breakout points to confirm routing
6. Remove fixture and install actual DART module with confidence

**This process prevents:**
- Installing SoMs on boards with power supply issues
- Damaging expensive modules during initial bring-up
- Wasting time troubleshooting with live hardware

### Development & Prototyping
- First-power validation of new carrier board designs
- Power supply characterization and optimization
- Signal routing verification before ordering production quantities

### Troubleshooting & Repair
- Quickly diagnose power delivery issues on returned boards
- Verify connector integrity and pin continuity
- Isolate motherboard issues from SoM problems

---

## Technical Specifications

**Form Factor:**
- Matches Variscite DART-MX91/93/95 module dimensions
- PCB: 55.18mm × 30.11mm
- 2-layer board
- Standard DART connector footprint

**Power Indicators:**
- 4× green LEDs for visual power validation
- Current-limiting resistors sized for clear visibility
- Low power consumption (<50mA total)

**Test Points:**
- 3.3V and GND loops for electronic load connection
- Optional 0.1" header positions for signal access

**Signals Available:**
- USB1 differential pair (D+/D-)
- USB2 differential pair (D+/D-)
- I2C1 bus (SDA/SCL)
- UART1 (TX/RX)

---

## Hardware Design

### PCB Renders

**Top View:**

<img src="docs/images/top-3d-render.png" width="600">

*Test fixture top side showing LED indicators and optional header positions*

**Bottom View:**

<img src="docs/images/bot-3d-render.png" width="600">

*Bottom side with DART connector*

### Design Files

**Available Documentation:**
- **Schematic:** [View PDF](hardware/pcb/schematic-final.pdf)
- **Gerber Files:** [Download ZIP](hardware/pcb/gerbers/gerber-files-final.zip)

**PCB Specifications:**
- 2-layer board
- Dimensions: 55.18mm × 30.11mm
- Matches DART-MX91/93/95 form factor
- Standard PCB thickness and copper weight

---

## Assembly Options

**Minimal Configuration (Most Common):**
- 4× LEDs with current-limiting resistors
- Test loops for power validation
- **Use breakout positions as test points only** (no headers populated)

**Full Configuration:**
- All LEDs and indicators
- Populated 0.1" headers for all signal breakouts
- Useful for extended troubleshooting or development

**Most production testing uses minimal configuration** - LEDs provide quick visual validation, and signal test points are sufficient for occasional continuity checks.

---

## How to Use

### Basic Power Validation

1. **Install fixture** in DART connector on your carrier board
2. **Apply power** to carrier board
3. **Check LEDs:**
   - ✅ VBAT LED on: 3.3V main power present
   - ✅ USB1_VBUS LED on: USB1 power present (if used in design)
   - ✅ USB2_VBUS LED on: USB2 power present (if used in design)
   - ✅ VCC_MX95 LED on: Additional 3.3V present (DART-MX95 only)

4. **If any LED fails to illuminate:** Power supply issue on carrier board - do NOT install SoM

### Power Supply Load Testing

1. Install fixture in DART connector
2. **Connect electronic load** to 3.3V and GND test loops
3. **Set load current** to expected SoM draw (typically 500mA-2A depending on application)
4. **Verify voltage regulation:** 3.3V should remain stable under load
5. **Check for voltage drop** across connector and PCB traces
6. **Measure ripple** if needed for sensitive applications

### Signal Continuity Testing

1. Use multimeter or oscilloscope
2. **Probe breakout test points** (or populated headers)
3. **Verify continuity** from DART connector pins to carrier board routes
4. **Check for shorts** between differential pairs (USB) or bus lines (I2C)

---

## Impact & Production Use

**Production Validation:**
- Used to test **every production motherboard** before SoM installation
- Catches power supply issues before expensive modules are at risk
- Reduces debugging time by 80%+ compared to troubleshooting with live SoM
- Enables confident high-volume production runs

**Cost Savings:**
- Prevents damage to $100-300 DART modules
- One $20 test fixture replaces risking expensive hardware
- Reusable across unlimited production units

**Quality Assurance:**
- Ensures every shipped board has verified power delivery
- Validates connector integrity and pin continuity
- Reduces field failures and customer returns

---

## Design Approach

**Production-Focused Tool:**
This fixture was developed from real production testing needs - validating hundreds of custom DART carrier boards required a fast, reliable, reusable test method.

**Key Design Decisions:**
- **Visual indicators over automated testing:** Green LEDs provide instant go/no-go validation
- **Test loops for load testing:** Power supply issues are the #1 cause of motherboard failures
- **Optional breakout headers:** Keep cost low, populate only when needed for troubleshooting
- **Exact DART form factor:** Ensures connector mechanical validation matches production use

---

## Applications

**Industries Using Custom DART Carrier Boards:**
- Industrial automation and control systems
- Medical device embedded computing
- Edge computing and IoT gateways
- Automotive infotainment and telematics
- Robotics and machine vision

**This fixture is essential for any production environment** using Variscite DART modules with custom carrier board designs.

---

## Future Enhancements

Potential improvements for future versions:
- Automated LED monitoring with pass/fail output signal
- Built-in current measurement on power rails
- USB signal integrity test patterns
- Pogo pin version for bed-of-nails testing fixture

---

## Related Projects

This test fixture is part of a broader hardware validation and production testing methodology for embedded Linux systems based on NXP i.MX9x processors.

---

## Contact

Professional hardware engineering tool used in production testing. For technical questions or collaboration inquiries, please contact via GitHub.

---

*This project demonstrates production-focused test fixture design, hardware validation methodology, and quality assurance practices for System-on-Module based products.*
