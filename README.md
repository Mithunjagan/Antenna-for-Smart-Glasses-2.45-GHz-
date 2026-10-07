# 2.45 GHz Antenna for Smart Glasses

**Design by MithunKumar J**

My project is a compact inverted-F antenna (IFA) for the 2.45 GHz band, designed on a 50 × 6 mm FR4 PCB for integration into a smart-glasses temple. The repository contains the CST model, native simulation results, antenna architecture and design documentation.

The current free-space CST result is **S11 = −24.73 dB at 2.45 GHz**, **input impedance = 50.70 + j5.81 Ω**, and **sampled peak realized gain = 1.95 dBi**. All sampled points in the 2.38–2.52 GHz design band satisfy S11 < −10 dB.

## Project files

- [CST antenna project](cst/antenna.cst)
- [Native S11 data](results/S11_native_dB.txt)
- [50 Ω Touchstone data](results/S_parameters.s1p)
- [Realized-gain farfield data](results/farfield_2.45_realized_gain.txt)
- [Functional antenna architecture](docs/architecture.md)
- [Simulation details and result definitions](docs/simulation-evidence.md)
- [Hardware validation plan](docs/hardware-validation.md)

## Functional architecture

![RF path of the smart-glasses antenna](docs/diagrams/rf-path.svg)

The 50 Ω feed excites the IFA through an ideal 1.8 pF series matching capacitor. The PCB ground provides the return-current path. The radio interface and complete glasses assembly require further integration work.

## CST results

These values belong to the completed **55,440-cell free-space model**, using CST Studio Suite 2026.4 Learning Edition and its Time Domain HEX solver. Radiation metrics refer to the 2.45 GHz monitor.

| Parameter | Result |
|---|---:|
| S11 at 2.45 GHz | −24.729083 dB |
| Input impedance at 2.45 GHz | 50.7027 + j5.8097 Ω |
| VSWR at 2.45 GHz | 1.12318 |
| Sampled peak realized gain | 1.94792 dBi |
| Radiation efficiency | 94.4282% |
| Total efficiency | 94.1096% |
| Minimum sampled S11 | −25.386804 dB at 2.4625001 GHz |
| Worst sampled S11 in 2.38–2.52 GHz | −15.315246 dB |
| Approximate −10 dB bandwidth | 2.312221–2.713050 GHz |
| Fractional impedance bandwidth | 16.2773% |
| Actual mesh cells | 55,440 |

Impedance and VSWR are calculated from native complex S11 with a 50 Ω reference. Efficiency percentages are converted from native dB values. Gain is the maximum of the native realized-gain export on a 5° angular grid. Band edges use interpolation at the −10 dB crossings; fractional bandwidth is `(fH − fL) / fmin × 100`, with fmin = 2.4625001 GHz.

## Antenna dimensions

| Feature | Dimension |
|---|---:|
| PCB | 50 × 6 mm |
| FR4 core thickness | 0.8 mm |
| Copper thickness per face | 0.035 mm |
| Radiator length | 23.6 mm |
| Radiator trace width | 0.7 mm |
| Ground length | 28 mm |
| Short offset / feed offset | 9 mm / 6 mm |
| Feed width | 1.5 mm |
| Copper edge clearance | 0.3 mm |
| Via pad / drill diameter | 0.7 mm / 0.3 mm |
| Via plating thickness | 0.025 mm |
| Matching capacitor | Ideal 1.8 pF series element |
| Housing wall / air spacing | 1 mm / 0.25 mm |
| Modeled housing footprint | 52 × 8 mm |

The short position is `x = ground length − short offset`; the feed tap is `x = ground length − short offset + feed offset`, giving x = 25 mm. The discrete feed represents a local excitation rather than a completed connector footprint.

FR4 uses relative permittivity 4.4 and loss tangent 0.02. Copper conductivity is 5.8 × 10⁷ S/m. The housing plastic uses nominal relative permittivity 3 and loss tangent 0.01. Soldermask is omitted.

## Simulation setup

- Solver: CST Time Domain HEX.
- Frequency sweep: 1.0–3.5 GHz.
- Field and farfield monitors: 2.4, 2.45 and 2.4835 GHz.
- Excitation: ideal 50 Ω discrete feed with a 1.8 pF series capacitor.
- Environment: free space with open boundaries and a local plastic housing.

The capacitor has no modeled ESR, ESL, package or pads. A physical connector/coax, solder joints, battery, electronics, hinge and full glasses frame are not represented.

## Mesh study

| Model | Actual cells | S11 at 2.45 GHz | Minimum-S11 frequency |
|---|---:|---:|---:|
| First verification mesh | 35,438 | −23.464302 dB | 2.4549999 GHz |
| Intermediate mesh | 41,013 | −24.163222 dB | 2.4549999 GHz |
| Current mesh | 55,440 | −24.729083 dB | 2.4625001 GHz |

The last completed resonance shift is **7.5 MHz**, exceeding the 5 MHz convergence criterion. A subsequent refinement exceeded the Learning Edition's 100,000-cell limit. Its [native failure log](results/mesh-study/refinement-limit/Model.log) is retained. Mesh convergence remains incomplete.

## Open the CST project

Download or clone the complete repository, then open [`cst/antenna.cst`](cst/antenna.cst) in CST Studio Suite. Keep the neighboring [`cst/antenna/`](cst/antenna/) folder with the project: it contains the native model and result database.

Inspect the saved S-parameter and efficiency results and the 2.45 GHz farfield monitor in CST. A new solve or finer mesh requires an appropriate CST installation and sufficient licensed mesh capacity.

## Hardware status

The free-space design meets the reported matching target. Before fabrication, the remaining work is to define the physical feed and matching component, complete mesh convergence, evaluate full-frame and head loading, assess SAR and manufacturing tolerances, and measure a prototype. No measured prototype performance or completed hardware release is claimed.

## Repository layout

```text
cst/antenna.cst          Native CST antenna project
cst/antenna/            Native model and result database
results/                Native S11, Touchstone, efficiency and farfield exports
results/mesh-study/     Mesh-comparison data and native logs
docs/                   Antenna architecture and engineering documentation
docs/diagrams/          Functional RF and design-process diagrams
```
