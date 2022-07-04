# PLC Device Mapping Specification
The Mitsubishi FX5U PLC used for the Congestion Reducing Device (CRD) and Energy Management System (EMS) applications makes use of a globally address space for storage of variables,interfacing with (hardware) inputs and outputs and other (protocol) interfaces. Although not enforced by the development environment, we should always assign a description for any used address recorded in the "Common Device Comment". This document specifies which regions of the address space is reserved for the different application components in the PLC software

# Device registers (16 bit word addressing) Dxxx

| Start | End | Description |
|-|-|-|
| D0 | D39 | Modbus mapping A1.1 (U1.1) |
| D40 | D79 | Reserved |
| D80 | D119 | Modbus mapping A1 (U2.1 and U2.2) |
| D130 | D139 | Communication counters |
||||
| D1000 | D1099 | Converted values from A1.1 (U1.1) |
| D1100 | D1199 | Reserved |
| D1200 | D1299 | Converted values from A1 (U2.1 and U2.2) |
||||
| D2000 | D2099 | Test 1 Values |
| D2100 | D2199 | Test 2 Values |
| D2200 | D2299 | Test 3 Values |
||||
| D2500 | D2599 | ATEPS |

# Markers (1-bit addressing) Mxxxx
| Start | End | Description |
|-|-|-|
| M0 | M39 | Modbus mapping A1.1 (U1.1) |
| M0 | M79 | Reserved
| M80 | M119 | Modbus mapping A1 (U2.1 and U2.2) |
| M200 | M249 | Test Controllers |
| M250 | M299 | ATEPS |

# Digital inputs (Xxxxx)
| Start | End | Description |
|-|-|-|
| X0 | | A1 (U2.1 and U2.2) Running |
||||
| X10 | | A1.1 (U1.1) Running |

# Digital outputs (Yxxxx)
| Start | End | Description |
|-|-|-|
| Y0 | | A1 (U2.1 and U2.2) Precharge |
| Y1 | | A1 (U2.1 and U2.2) Run (DIN1) |
| Y2 | | A1 (U2.1 and U2.2) MCB Open (DIN2) |
| Y3 | | A1 (U2.1 and U2.2) Reset Faults (DIN5) |
||||
| Y10 | | A1.1 (U1.1) Precharge |
| Y11 | | A1.1 (U1.1) Run (DIN1) |
| Y12 | | A1.1 (U1.1) MCB Open (DIN2) |
| Y13 | | A1.1 (U1.1) Reset Faults (DIN5) |








