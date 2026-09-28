# CMOS Low Noise Amplifier Analysis Using S-Parameters

A 2.45 GHz CMOS Low Noise Amplifier (LNA) designed and simulated with an RF simulator, using a common-source NMOS topology with inductive source degeneration. The design is evaluated with S-parameter analysis (S11, S21, S12, S22) and gain metrics (GA, GP, GT) from 0 to 5 GHz.

> Academic project, Department of Electronics and Communication Engineering, SRM University-AP (Neerukonda, Mangalagiri Mandal, Guntur, Andhra Pradesh), Academic Year 2025-2026.

## Contents
- [Overview](#overview)
- [Schematic](#schematic)
- [Circuit components](#circuit-components)
- [Results](#results)
- [Repository structure](#repository-structure)
- [How to reproduce](#how-to-reproduce)
- [Advantages and limitations](#advantages-and-limitations)
- [Future work](#future-work)
- [Applications](#applications)
- [References](#references)

## Overview
The LNA is the first active block in a receiver chain, so its noise and matching directly set receiver sensitivity. This design targets the 2.45 GHz ISM band (Wi-Fi, Bluetooth) in CMOS for low power, low cost and easy integration.

**Design highlights**
- Common-source NMOS amplifier (M1) with source inductor (L3) for degeneration
- Second NMOS (M2) and resistor R0 for biasing
- Inductive input matching (L2) and drain inductor load (L1)
- 50 ohm source and load ports

## Schematic
![LNA schematic](schematic/lna_schematic.png)

## Circuit components
| Component | Role |
|---|---|
| M1 (NMOS) | Main common-source amplifying device |
| M2 (NMOS) | Biasing / current-source element keeping M1 in saturation |
| C1 | Input DC-blocking (coupling) capacitor |
| C4 | Output coupling capacitor |
| C3 | Bypass capacitor, AC ground for the bias network |
| L1 | Drain inductor, load that raises voltage gain |
| L2 | Input inductor, impedance matching |
| L3 | Source inductor, degeneration (input match, noise, stability) |
| R0 | Gate bias resistor |
| VDD | DC supply |
| PORT0 / PORT1 | RF input / output ports (50 ohm) |

Values visible in the schematic: VDD = 1.2 V, gate bias = 600 mV, R0 = 50 kOhm, W = 60 um (nmos1v devices).
<!-- TODO: add the final L1, L2, L3, C1, C3, C4 values here after checking your simulator schematic. -->

## Results
Simulation: S-parameter analysis, 0-5 GHz.

| Metric at ~2.45 GHz | Value |
|---|---|
| S11 (input return loss) | about -18 dB (-17.98 dB at 2.456 GHz) |
| GA (available gain) | about 19.5 dB |
| GT (transducer gain) | about 7.5 dB |
| S12 (reverse isolation) | roughly -50 dB, very low |
| S22 (output match) | acceptable, not fully optimized |

GT is lower than GA because of mismatch losses at the output.

### S11, S21, S12
![S11 S21 S12](results/s11_s21_s12.png)

### All S-parameters
![All S-parameters](results/all_s_parameters.png)

### Gain comparison (GA, GP, GT)
![Gain comparison](results/gain_comparison.png)

### Performance at the operating frequency
![Performance at 2.45 GHz](results/performance_at_2p45GHz.png)

## Repository structure
```
cmos-lna-sparameter-analysis/
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   └── LNA_Report.pdf        # full project report
├── schematic/
│   └── lna_schematic.png
└── results/
    ├── s11_s21_s12.png
    ├── all_s_parameters.png
    ├── gain_comparison.png
    └── performance_at_2p45GHz.png
```

## How to reproduce
1. Recreate the schematic (see image and component table) in your RF simulator (the report references ADS-style S-parameter analysis).
2. Apply VDD = 1.2 V and the gate bias, with 50 ohm ports.
3. Run an S-parameter simulation from 0 to 5 GHz.
4. Plot S11, S21, S12, S22 in dB and GA, GP, GT.
5. Compare the S11 dip and gain peak near 2.45 GHz with the plots above.

## Advantages and limitations
**Advantages:** good input match (S11 < -10 dB), stable operation, excellent reverse isolation, low power and low cost in CMOS, compact design, easy integration.

**Limitations:** moderate gain, S22 not fully optimized, narrow bandwidth around 2.45 GHz, sensitivity to component values and process variation, large inductor area on chip, noise figure not yet quantified or minimized.

## Future work
- Simulate and report noise figure (NF) and stability factor (K / mu)
- Optimize the output matching network to improve S22 and GT
- Increase gain, for example with a cascode stage
- Add process-corner and temperature sweeps
- Add linearity metrics (P1dB, IIP3) and power consumption

## Applications
Wi-Fi and Bluetooth receivers, RF front ends, mobile devices, IoT nodes, GPS receivers, wireless sensor networks, and satellite and radar receivers.


## References
1. B. Razavi, *RF Microelectronics*, 2nd Ed., Pearson Education
2. D. M. Pozar, *Microwave Engineering*, 4th Ed., Wiley
3. T. H. Lee, *The Design of CMOS Radio-Frequency Integrated Circuits*, Cambridge University Press
4. ADS (Advanced Design System) documentation
