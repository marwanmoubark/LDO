# Low Dropout Regulator (LDO) — 65 nm CMOS

A custom low-power LDO regulator designed and simulated in 65 nm CMOS technology
using Cadence Spectre. The core error amplifier is a two-stage OTA sized using a
gm/ID-based methodology.

---

## Team
| Name | ID |
|------|----|
| Marwan Mohamed Mobarak Soliman | 91240727 |
| Mahmoud Ahmed Mahmoud Ahmed | 91240706 |
| Ahmed Mohamed Abdelnaby | 9220090 |

---

## Specifications

| Parameter | Value |
|-----------|-------|
| Technology | 65 nm CMOS |
| Supply Voltage (VDD) | 1.2 V |
| Output Voltage Range | 0.75 V – 1.05 V |
| Output Step Size | 50 mV |
| Total Quiescent Current | < 47 µA |
| Simulator | Cadence Spectre |
| Process Corners | TT, SS, FF |

---

## Architecture

### OTA (Error Amplifier)
- **Topology:** Two-stage OTA with Miller compensation
- **Input pair (M1–M2):** NMOS high-Vth (nch_hvt) for higher Early voltage
- **Load (M3–M4):** PMOS current mirror
- **Tail current source (M5):** Biased at gm/ID = 13

### Device Sizing Summary

| Transistor | W (µm) | L (µm) | ID (µA) | gm/ID (S/A) |
|------------|--------|--------|---------|-------------|
| Input Pair | 10 | 0.8 | 10 | 16 |
| PMOS Load | 3 | 0.8 | 10 | 15 |
| Tail CS | 4 | 0.6 | 20 | 13 |

### LDO
- **Pass transistor:** PMOS (W = 10 µm, L = 120 nm)
- **Feedback network:** Programmable R1 (0 – 22.5 kΩ), fixed R2 = 30 kΩ
- **Reference voltage:** VREF = 0.6 V
- **Output equation:** `V_OUT = VREF × (1 + R1/R2)`

---

## Simulation Results

### OTA Performance

| Parameter | Result |
|-----------|--------|
| DC Gain | 38.5 dB |
| GBW | 5.57 MHz |
| Phase Margin | 89.9° |
| CMRR | 70 dB |
| CMIR Low / High | 0.62 V / 1.2 V |
| Current Consumption | 20 µA |

### LDO Performance

| Parameter | Result |
|-----------|--------|
| Output Range | 0.75 V – 1.05 V |
| Dropout Voltage | ~28 mV |
| PSRR | −58.6 dB |
| Total Quiescent Current | 46.83 µA |
| PVT Accuracy | ±1.5 mV (±0.2%) |
| Phase Margin (closed-loop) | > 60° |

### Programmable Output Voltages

| Step | R1 (kΩ) | V_OUT (V) |
|------|---------|-----------|
| 0 | 7.5 | 0.75 |
| 1 | 10.0 | 0.80 |
| 2 | 12.5 | 0.85 |
| 3 | 15.0 | 0.90 |
| 4 | 17.5 | 0.95 |
| 5 | 20.0 | 1.00 |
| 6 | 22.5 | 1.05 |

---

## Design Methodology
- **gm/ID-based sizing** for systematic trade-off between gain, bandwidth, and power
- **Miller compensation** for stability under capacitive loading
- **PVT analysis** across TT/SS/FF corners and temperature sweep (−25°C to 65°C)
- **DC operating point** verification to confirm all transistors in saturation

---

## Tools
- **Schematic & Simulation:** Cadence Virtuoso + Spectre
- **Analyses:** DC, AC, Transient, PVT corner sweep
