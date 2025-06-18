
# Standard Cell Library

A Standard Cell Library is a collection of reusable, pre-designed logic components like logic gates, multiplexers, and latches. These cells are used as fundamental building blocks in ASIC and SoC design during the synthesis and physical layout stages. In this project, each standard cell layout was carefully implemented using Euclidean path routing, ensuring minimal wire length, better area efficiency, and improved timing.

## Euclidean Path Routing
Euclidean path routing involves connecting components using the shortest possible path that adheres to the geometric constraints (typically 45° or 90° angles). Unlike Manhattan routing (which uses only horizontal and vertical segments), Euclidean routing allows more direct paths, leading to:
- Shorter interconnects
- Reduced parasitic capacitance
- Lower delay
- Optimized power consumption
- Compact and cleaner layout geometry
All the layouts below were designed with Euclidean routing strategy to ensure optimized signal flow and design rule compliance.

## Inverter

### Initial Layout: 
Drafted with a single PMOS/NMOS pair in a shared well. The first cut left body ties unconnected and diffusion taps too far apart, triggering well‐tie and minimum‐distance DRC violations.
### Core Layout: 
Added proper body ties (PMOS → VDD, NMOS → GND), aligned diffusion edges for minimum parasitics, and widened the VDD/GND rails. After re routing the input/output with the shortest Manhattan paths, the cell cleared all DRC and LVS checks and was saved as a reusable primitive.
### HDRC View:
A hierarchical DRC–only view now lets higher level schematics drop multiple inverter instances while verifying rule compliance without repeating LVS every time.

![Inverter Schematic](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/inverter%204x%20schematic.png)
![Inverter Layout ](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/inv%20layout.png)
![Inverter Layout Core](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/inv%20layout%20core.png)
![Inverter Layout hdrc ](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/inv%20layout%20hdrc.png)


## Inverter 4X
### Initial Layout: 
Created by scaling the transistor widths 4 ×. Early placement violated poly to diffusion spacing and exceeded maximum diffusion width limits, producing seven DRC errors.
### Core Layout:
 Split the wide devices into fingers, inserted additional diffusion contacts, and re centered the output pin to balance RC loading. With body ties re positioned to meet density rules, the 4× inverter passes full DRC/LVS and is packaged as a drive strength variant aligned to the standard cell row height.
### HDRC View:
Provides a lean DRC only snapshot so large clock or buffer chains can instantiate the 4× cell repeatedly without incurring schematic equivalence runtimes.

![ Inverter 4X Schematic](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/inverter%204x%20schematic.png)
![ Inverter 4X Layout ](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/inverter%204x%20layout.png)
![ Inverter 4X Layout Core](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/inverter%204x%20layout%20core.png)
![Inverter 4X Layout hdrc](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/inverter%204x%20layout%20core.png)


## 2 Input NAND Gate

### Initial Layout:
Implemented with series NMOS and parallel PMOS networks. Initial draft omitted a well tap for the stacked NMOS region and violated poly extension rules at the shared input, leading to five DRC flags.
### Core Layout: 
Added a grounded well tap between the NMOS devices, ensured all poly extensions met minimum length, and routed A/B inputs with equal path lengths to minimize skew. After cleanup, the cell achieved clean DRC and LVS results and was encapsulated for library use.
### HDRC View: 
The hierarchical DRC view enables rapid top level verification of combinational logic blocks populated with NAND instances, catching rule infractions while skipping redundant LVS comparisons

![ 2 Input NAND Gate Schematic](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/nand%20schematic.png)
![2 Input NAND Gate Layout](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/nandlayout.png)
![2 Input NAND Gate Layout Core](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/nand%20layout%20core.png)
![2 Input NAND Gate Layout hdrc](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/nand%20layout%20hdrc.png)


## EXOR Gate

### Initial Layout: 
The EXOR gate was designed using CMOS logic. In its initial version, body terminals were not connected, resulting in three DRC errors due to unconnected wells or substrate violations.
### Core Layout: 
After proper body connections (PMOS to VDD, NMOS to GND) were added and signal paths routed using Euclidean shortest path, the layout was encapsulated as a reusable cell. It successfully passed DRC and LVS checks.
### HDRC View: 
A hierarchical DRC view was created to validate multiple instances of the EXOR cell in higher-level designs. This view performs only DRC verification, ensuring layout rule compliance without re-checking schematic equivalence. 

![EXOR Gate Schematic](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/exor%20schematic.png)
![EXOR Gate Layout ](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/exor_layout.png)
![EXOR Gate Layout Core](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/exor_core.png)
![EXOR Gate Layout hdrc](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/exor_hdrc.png)

## Multiplexer (2:1 MUX)

### Initial Layout: 
The MUX layout, built using transmission gates, initially lacked body connections and failed DRC with three violations.
### Core Cell: 
After resolving body connections and rerouting signals and control lines using Euclidean path, the core layout was verified successfully with no DRC or LVS errors. This optimized layout contributes to minimal propagation delay.
### HDRC Verification: 
A hierarchical layout view was used to check the MUX when instantiated multiple times. DRC ensured proper spacing and geometry compliance for all instances. 

![Multiplexer (2:1 MUX) Schematic](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/mux%20schematic.png)
![Multiplexer (2:1 MUX) Layout ](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/mux_layout.png)
![Multiplexer (2:1 MUX) Layout Core](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/mux_core.png)
![Multiplexer (2:1 MUX) Layout hdrc](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/mux_hdrc.png)

##  D-Latch

### Initial Layout: 
The D-Latch was implemented using CMOS inverters and transmission gates. The preliminary version failed DRC with three body connection errors.
### Corrected Core: 
Once body terminals were tied appropriately and routing was redone using Euclidean shortest paths, the D-Latch passed both DRC and LVS checks and was instantiated as a clean core cell.
### Hierarchical Validation: 
The D-Latch was verified using HDRC mode in a larger system context, confirming that all instances meet physical design rules. 

![D-Latch Schematic](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/dlatch%20schematic.png)
![D-Latch Layout ](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/d_latch.png)
![D-Latch Layout Core](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/d_latch_core.png)
![D-Latch Layout hdrc](https://github.com/Deepthi-S-G/Standard-Cell-Layout-Design-UMC-180-/blob/main/Images_of_Standard_Cell_Library/d_latch_hdrc.png)

## Summary of Workflow with Euclidean Path Routing

1.	Schematic Design: Develop transistor-level schematics for each cell (EXOR, MUX, D-Latch).
2.	Layout Drafting: Draw layout in Cadence Virtuoso using Euclidean path routing — prioritizing the shortest possible interconnects and minimal overlap.
3.	Body Connection Integration: Connect PMOS and NMOS bodies to appropriate wells and supply rails.
4.	DRC and LVS Checks: Verify compliance with design rules (DRC) and schematic equivalence (LVS).
5.	Core Cell Creation: Save verified layouts as standard cell cores for reuse.
6.	HDRC View: Perform hierarchical DRC checks to ensure scalability and integrity across multiple cell instances.
7.	Path Optimization: Confirm that all interconnections use Euclidean routing, minimizing layout area, delay, and power.

## Conclusion

- The development of the Standard Cell Library demonstrated the successful design and verification of essential digital logic components—EXOR, 2:1 Multiplexer, and D-Latch—using Cadence Virtuoso with Euclidean path-based routing. Each cell was initially constructed at the transistor level and rigorously verified through Design Rule Check (DRC) and Layout Versus Schematic (LVS) validation.
- In the early layout stages, all three cells showed DRC errors primarily due to missing body connections. After systematically resolving these issues and optimizing the routing paths using the Euclidean path strategy, each layout was instantiated as a core cell. These core cells successfully passed both DRC and LVS checks, ensuring their functional correctness and physical integrity.
- Further, the Hierarchical DRC (HDRC) views were created to evaluate the reuse of these cells in larger hierarchical designs. This helped verify that multiple instantiations of the same cell do not introduce any new layout violations, making the cells scalable and integration-ready.
- The use of Euclidean routing significantly improved the compactness, signal integrity, and routing efficiency of the layouts, thereby enhancing their suitability for standard cell libraries in ASIC and SoC environments. These verified standard cells now serve as reliable building blocks for constructing more complex digital systems with optimized area, power, and timing characteristics.
