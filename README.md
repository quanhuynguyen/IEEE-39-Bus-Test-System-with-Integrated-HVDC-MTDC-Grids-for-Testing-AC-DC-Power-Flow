# IEEE 39-Bus Test System with Integrated HVDC/MTDC Grids for Testing AC-DC Power Flow

This repository provides a version of the IEEE 39-bus (New England) test system, and extended data for multiple integrated HVDC and MTDC grid configurations. The platform is specifically designed to support scalable, co-simulation-based AC–DC power flow studies using industry-grade AC solvers and an external DC solver.

--- AC-DC System Description:
1) Baseline System
   - Based on the standard IEEE 39-bus system widely used for transmission-level dynamic and steady-state studies.
   - Preserves the original AC topology, generation dispatch structure, and load distribution for benchmarking consistency.
3) Integrated HVDC and MTDC Configurations
   - Point-to-point HVDC links embedded at selected AC buses.
   - Multi-terminal DC (MTDC) grids with configurable topologies (radial, meshed, hybrid).

--- Power Flow Data of the AC-DC Systems:
1) INPUTS

   AC grid:
   - The AC grid is based on the IEEE 39-bus system, and is represented in file IEEE39bus_Modified_v35.raw (if using PSSE) or IEEE39bus_Modified_v35.pwb (if using PowerWorld).  This is     the model without HVDC grid addition.
   
   DC grid:
   - DC buses are included in DC_Buses.csv.
   - DC line resistances are included in DC_Lines.xlsx.
   - Converter data is included in DC_Converters.csv, including interconnected AC and DC buses, converter ratings, reactive power control mode, droop parameters, current limit, and
   current-limiting strategies.
      - Reactive power control modes (1: constant ac voltage, 2: constant reactive power, 3: constant power factor)
      - Pac-Vdc droop control depends on droop coefficient (0: cosntant Vdc control, 10^6: cosntant Pac control, others: normal droop with nonzero power deviation)
   - Converter losses: For solving AC-DC power flow, converter loss can be calculated as follows:
      Loss = a +b * abs(I_ac) + c * abs(I_ac)**2
      where a = 0.01549752, b = 0.000474217, c = 0.003306, and I_ac is the AC-side converter current in p.u w.r.t Sbase = 100 MVA.

2) OUTPUTS

   AC grid:
   - The output AC grid with equivalent generators representing HVDC converters and corresponding dispatch is represented in ac_Equivalent_MTdcConverters_scaleLoad.sav. Note that
   converters are operating in ac-voltage control mode instead of reactive power control mode for this case study.

   DC grid:
   - The DC voltages are included in file xSolution_Voltages_HVdc1.csv
   - The DC line power is included in file xSolution_LinePowers_HVdc1.csv
   - The AC-side and DC-side power of converters is included in  xSolution_Converter_HVdc.csv. Nothe that the AC-side and DC-side power values are not the same because of converter
     losses.


