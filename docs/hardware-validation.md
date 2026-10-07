# Hardware validation plan

The current design passes simulated free-space input matching. A physical implementation still needs a component model, a defined feed, integration checks and measurements.

## Current release status

| Check | Status |
|---|---|
| Native free-space S11 over 2.38–2.52 GHz | Sampled target passes |
| Actual copper material and feed connectivity | Checked in the completed CST run |
| Mesh convergence | Incomplete; further refinement hit the license limit |
| Physical 1.8 pF capacitor, footprint and parasitics | Not modeled |
| Connector/coax, solder and PCB finish | Not modeled |
| Full glasses frame, electronics, hinge and battery | Not modeled |
| Tuned on-head matching, efficiency and gain | Not verified |
| Tuned on-head SAR | Not verified |
| Manufacturing tolerances and prototype measurements | Pending |
| Final fabrication release | Not approved |

## Complete the electromagnetic model

Select the feed interface and actual capacitor before defining the final PCB footprint. Replace the ideal RLC element with the selected physical implementation, including pad geometry, ESR/ESL and available measured or manufacturer-supplied component data. Include the actual connector/coax and solder geometry.

Confirm the FR4 stack-up, copper, finish and soldermask inputs. The PCB is 50 × 6 mm, while the modeled housing footprint is 52 × 8 mm; check the finished mechanical envelope with the actual glasses design.

Use sufficient licensed mesh capacity to complete convergence. Keep geometry, material inputs and solver settings fixed when comparing successive meshes. Check the native cell count and mesh controls, not only the requested density.

Add the actual glasses structure and intended head-loading conditions. Run matching, radiation and SAR studies with a documented accepted-power normalization and suitable phantom/material models. Record native results and failed cases without replacing missing outputs with estimates.

## Verify the prototype

1. Inspect copper dimensions, via pads/drills, stack-up and the assembled feed/matching element against the EM geometry.
2. Calibrate a 50 Ω VNA at the chosen reference plane, preserve complex S11 as Touchstone, and record calibration, power, averaging and fixture conditions.
3. Measure free-space matching and repeat after reconnecting; control cable placement and fixture effects.
4. Repeat under controlled integration and head-phantom conditions, with documented spacing and phantom properties.
5. Measure radiation patterns, realized gain and efficiency with a suitable calibrated setup. Preserve coordinate-system and polarization definitions.
6. Complete exposure evaluation using an appropriate calibrated SAR setup and applicable test protocol before making a compliance claim.
7. Investigate discrepancies using as-built dimensions, material inputs, connector/cable effects and component parasitics.

## Fabrication status

No final Gerbers for the tuned capacitor design are included. A physical matching footprint, completed RF and assembly checks, and prototype measurements are required before fabrication release.
