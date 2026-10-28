# 3D Flow in a Wedge-Plate Junction

Simulation of a pressure-driven three-dimensional turbulent boundary layer in Simcenter STAR-CCM+, compared against the wind-tunnel measurements of Anderson & Eaton (ERCOFTAC Classic Collection, Case 002).

Course project, M.Sc. Computational Methods in Engineering, Otto-von-Guericke-Universität Magdeburg.

## Geometry
<img width="619" height="363" alt="3D view of full geometry" src="https://github.com/user-attachments/assets/db06f958-79de-4edf-970c-711e68a18a0e" />

## Summary
A 90° wedge mounted between two parallel plates turns the oncoming flow and creates a spanwise pressure gradient. This pressure gradient skews the boundary layer on the test wall and makes it three-dimensional. 

A heated surface upstream of the wedge adds a thermal boundary layer.

I modelled the case in STAR-CCM+ with the SST k-ω turbulence model. I then compared the wall pressure coefficient and the wall-normal profiles of streamwise velocity, spanwise velocity and temperature with the experiment at stations S2, S3 and S4.

**After comparing the results from experiment and simulation:** Spanwise distribution of wall static Cp follows the experimental trend at all three stations. However, the simulation predicts a thinner velocity boundary layer and a thinner thermal boundary layer than measured, and it misses the spanwise (cross-flow) velocity component.

## Case description
 
The test section is a channel between two parallel walls 11.9 cm apart. The lateral walls follow a fourth-order polynomial in x, so the channel widens downstream. The wedge vertex sits on the centreline at x = 51.8 cm and turns the free stream by 45°. A 36 cm × 61 cm heated surface is placed on the test wall in front of the wedge. Measurements were taken through seven spanwise slots, S1–S7. The full specification is on the [ERCOFTAC case page](http://cfd.mace.manchester.ac.uk/ercoftac/doku.php?id=cases:case002).

| Parameter | Value |
|---|---|
| Fluid | Air, ν = 1.5 × 10⁻⁵ m²/s, ρ = 1.2 kg/m³ |
| Reference free-stream velocity | 16.391 m/s |
| Free-stream turbulence intensity | 0.2 % |
| Wall heat flux (heated surface) | 630 W/m² |
 
| Station | S1 | S2 | S3 | S4 | S5 | S6 | S7 |
|---|---|---|---|---|---|---|---|
| x (cm) | 7.6 | 22.9 | 38.1 | 45.7 | 53.3 | 61.0 | 68.6 |
 
**Coordinate note.** The computational domain starts at S1, so simulation x-coordinates are shifted by −7.6 cm relative to the experiment. For example, S2 lies at x = 0.153 m in the simulation and at x = 22.9 cm in the experiment. y is the wall-normal direction, and z is spanwise.

## Numerical setup
 
The simulation uses the full geometry rather than the half-geometry with a symmetry plane.
 
| | Setting |
|---|---|
| Solver | Simcenter STAR-CCM+, steady, 3D |
| Turbulence model | RANS, SST k-ω |
| Wall treatment | All y+ |
| Meshers | Surface remesher, polyhedral mesher, prism layer mesher |
| Base size | 0.01 m |
| Prism layers (configured) | 6 layers, 0.01 m total thickness, stretching 1.2 — **not generated in the final mesh** |
| Convergence | Residuals level off after ~500 iterations |
 
| Boundary | Condition |
|---|---|
| Inlet | Velocity inlet, 16.391 m/s, 300 K, turbulence intensity 0.2 %, length scale 0.01 m |
| Outlet | Pressure outlet, 0 Pa (gauge) |
| Heated surface | Wall, heat flux 630 W/m² |
| Other walls | No-slip, adiabatic |
 
The initial condition is fluid at rest at 300 K.

## Results
<img width="641" height="431" alt="Temperature vs Y-position in all measurement stations" src="https://github.com/user-attachments/assets/45e1eb3f-1153-4307-baf7-6bb8ff6c277b" />

<img width="624" height="362" alt="Wall static Cp vs Z-direction in all measurement stations" src="https://github.com/user-attachments/assets/8818273f-d5fe-40f0-8c4c-d1b20a69ec9a" />

<img width="652" height="412" alt="Velocity in Z-direction vs Y-position in all measurement stations" src="https://github.com/user-attachments/assets/b075393a-2955-4206-b1a2-d3cfbbffb494" />

<img width="632" height="417" alt="Velocity in X-direction vs Y-position in all measurement stations" src="https://github.com/user-attachments/assets/434619e3-e267-4666-88c5-800bc9362958" />

## Discussion and limitations
The pressure field is set mainly by the flow around the wedge, so a coarse near-wall mesh can still reproduce it reasonably well. The boundary layer quantities are much more sensitive. Without prism layers, only a few cells span the boundary layer. The stair-stepped shape of the simulated profiles shows this, and it is consistent with the thinner predicted boundary layers and the missing cross-flow.

## Data source and license
 
The experimental data is from the ERCOFTAC Classic Collection, Case 002, hosted by the University of Manchester and licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). This repository is shared under the same license.
 
Reference: S. D. Anderson and J. K. Eaton, "Experimental study of a pressure-driven, three-dimensional, turbulent boundary layer," *AIAA Journal*, 25, 1086 (1987).

## Repository structure
 
```
├── data/
│   ├── experiment,pdf      ERCOFTAC data
│   └── simulation.xlsx     line-probe exports from STAR-CCM+ and comparation with the EROFTAC data 
├── figures/             generated plots, geometry and mesh images
├── docs/                project presentation (PDF)

