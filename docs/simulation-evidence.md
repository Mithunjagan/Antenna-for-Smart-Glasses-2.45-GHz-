# CST simulation results

The performance in this repository belongs to the completed free-space IFA model, rather than a complete glasses assembly or a measured prototype.

## Native project and data

Open [`antenna.cst`](../cst/antenna.cst) with its neighboring [`antenna/`](../cst/antenna/) folder. The native solver log is [`Model.log`](../cst/antenna/Result/Model.log). The project file's SHA-256 is `bb04df3ad1560ef8d5153b14a0105a62b049d2284979cda56fb701f8f7e21e3c`.

The model uses CST Studio Suite 2026.4 Learning Edition, Time Domain HEX, a 1.0–3.5 GHz frequency sweep and field/farfield monitors at 2.4, 2.45 and 2.4835 GHz. The current completed mesh has 55,440 cells.

| Quantity | Native data | Definition |
|---|---|---|
| S11 | [S11 dB export](../results/S11_native_dB.txt) | Native sample at 2.45 GHz. |
| Impedance | [50 Ω Touchstone](../results/S_parameters.s1p) | Z = 50(1 + S11)/(1 − S11). |
| VSWR | [Complex S11](../results/S_parameters.s1p) | (1 + abs(S11))/(1 − abs(S11)). |
| Radiation efficiency | [Radiation-efficiency dB](../results/radiation_efficiency_native_dB.txt) | 100 × 10^(dB/10). |
| Total efficiency | [Total-efficiency dB](../results/total_efficiency_native_dB.txt) | 100 × 10^(dB/10); includes mismatch. |
| Realized gain | [2.45 GHz farfield](../results/farfield_2.45_realized_gain.txt) | 10 log10(maximum linear Abs(Grlz)); 5° angular sampling. |
| −10 dB band | [S11 sweep](../results/S11_native_dB.txt) | Linear interpolation of the crossings around the matched minimum. |

At 2.45 GHz, the model gives **−24.729083 dB S11**, **50.7027 + j5.8097 Ω**, **VSWR 1.12318**, **1.94792 dBi sampled peak realized gain**, **94.4282% radiation efficiency** and **94.1096% total efficiency**.

The sampled S11 minimum is −25.386804 dB at 2.4625001 GHz. The interpolated −10 dB band is approximately 2.312221–2.713050 GHz. Fractional bandwidth uses `(fH − fL)/fmin × 100`, yielding 16.2773%. Every sampled point in 2.38–2.52 GHz is below −10 dB; the worst value is −15.315246 dB.

## Numerical checks

The [35,438-cell](../results/mesh-study/35438-cells/) and [41,013-cell](../results/mesh-study/41013-cells/) runs retain their native logs and S11/efficiency exports. Only the current 55,440-cell run includes a complete project in this repository.

The minimum-S11 frequency changed from 2.4549999 to 2.4625001 GHz between the last two completed meshes: a 7.5 MHz shift, above the 5 MHz criterion. The [subsequent refinement log](../results/mesh-study/refinement-limit/Model.log) reports the Learning Edition's 100,000-cell limit. That refinement has no successful RF result. Convergence is incomplete.

## Interpretation limits

The 1.8 pF capacitor and 50 Ω feed are ideal elements. Physical parasitics and full glasses/head loading are not included. Radiation quantities are monitor samples; gain is a sampled directional maximum rather than a continuous maximum. No prototype measurement or completed SAR result is claimed.

The [file checksums](../results/file-checksums.sha256) cover the retained native project, database and exported data. The numerical data and native solver files are retained unchanged.
