# CHIP FLOW
Synthesis -> Floorplan -> Placement -> CTS -> Routing -> Signoff

## Files of each flow stage:
### Synthesis
Input: RTL 
Output: .lib 

.lib
- drive strenght
- cell delay
- slew and load tables
- timing and power model of standard cells

### Floorplan

LEF (Library Exchange Format)
- Abstract physical view of cells and macros
- Cell dimension
- pin location 
- metal layer

### PnR

DEF (Design Exchange Format)
- Cell placement
- power / ground routing
- net routing


## STA
This is not a stage but it's done as part of the process

SPEF (Standard Parasitic Exchange Format)
- Extracted parasitic RC from routing
- Contains: 
    - wire resistance
    - wire capacitance
    - coupling resistance


## Signoff
- GDSII: final file




