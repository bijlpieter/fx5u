# CRD Modbus Server Interface

## Overview
The CRD contains a PLC (Mitsubitshi FX5U) and 3 Vacon power converters: U1.1, U1.2 and U2. The power converter U1.2 is not used and therefore not available on the Modbus interface. Power converter U1.1 is connected to the 'left' grid (2MVA), and U2 is connected to the 'right' grid (630 KVA). The PLC can automatically control the power converters via predetermined tests and/or can act as an interface between external Modbus clients (e.g. HMI) and the power converters.

## Communication properties
| | |
|-|-|
| Communication hardware | Wired Ethernet, shielded CAT5e 100MBASE-T, up to 100 meter. |
| Communication protocol | Modbus TCP (over IP) |
| Server (Address:port) | ETV1-PLC1 (192.168.11.120:502) |
| Standard | [Modbus Application Protocol V1.1b3](https://modbus.org/docs/Modbus_Application_Protocol_V1_1b3.pdf) |
| Slave address | N.A. (Any from 0 ~ 255) |
| Supported function codes | 01, 02, 03, 04, 05, 06, 15, 16 |
| 32-bit floating point number encoding | IEEE754 |
| 32-bit word order | Little endian (bytes within a 16-bit word are ordered big endian as per Modbus specification) |
| Application data organization | Separate blocks (i.e. different function codes access different memory blocks) |

*Note that the data element (register) numbers are different from the PDU addresses used in the protocol (i.e. holding register (4)0001, input register (3)0001, discrete input (1)0001 and coil (0)0001 are encoded all as PDU address 0 in the protocol). Different register maps are accessed through use of different function codes.*

## Coil Map (read/write)
| Data element number | Content description |
|-|-|
| (0)0001 | U1.1 Connection Open Request (Rising edge, will clear automatically) |
| (0)0002 | U1.1 Charge DC (1) / Open CB (0) |
| (0)0003 | U1.1 Start (1) / Stop (0) |
| (0)0004 | U1.1 Reset Faults |
| (0)0005 | U1.1 FieldBus Control Enable |
|||
| (0)0101 ~ (0)0105 | Reserved for unused U1.2 |
|||
| (0)0201 | U2 Connection Open Request (Rising edge, will clear automatically) |
| (0)0202 | U2 Charge DC (1) / Open CB (0) |
| (0)0203 | U2 Start (1) / Stop (0) |
| (0)0204 | U2 Reset Faults |
| (0)0205 | U2 FieldBus Control Enable |
|||	
(0)1001 | Enable (1) / Disable (0) Test 1 Controller (will be cleared automatically when test completed) |
(0)1002 | Enable (1) / Disable (0) Test 2 Controller (will be cleared automatically when test completed) |
(0)1003 | Enable (1) / Disable (0) Test 3 Controller (will be cleared automatically when test completed) |


## Discrete Input Map (read-only)
| Data element number | Content description |
|-|-|
| (1)0001 | U1.1 Connection Open (PLC <-> Vacon communication) |
| (1)0002 | U1.1 Ready On |
| (1)0003 | U1.1 Ready Run |
| (1)0004 | U1.1 Running |
| (1)0005 | U1.1 Fault |
| (1)0006 | U1.1 Run Enabled |
| (1)0007 | U1.1 Quick Stop Not Active |
| (1)0008 | U1.1 Switch On Inhibit |
| (1)0009 | U1.1 Warning |
| (1)0010 | U1.1 At Reference |
| (1)0011 | U1.1 FieldBus Control Active |
| (1)0012 | U1.1 Above Limit |
| (1)0013 | U1.1 FB SW Bit 11 |
| (1)0014 | U1.1 FB SW Bit 12 |
| (1)0015 | U1.1 FB SW Bit 13 |
| (1)0016 | U1.1 FB SW Bit 14 |
| (1)0017 | U1.1 Watchdog |
|||
| (1)0101 ~ (1)0115 | Reserved for unused U1.2 |
|||
| (1)0201 | U2 Connection Open (PLC <-> Vacon communication) |
| (1)0202 | U2 Ready On |
| (1)0203 | U2 Ready Run |
| (1)0204 | U2 Running |
| (1)0205 | U2 Fault |
| (1)0206 | U2 Run Enabled |
| (1)0207 | U2 Quick Stop Not Active |
| (1)0208 | U2 Switch On Inhibit |
| (1)0209 | U2 Warning |
| (1)0210 | U2 At Reference |
| (1)0211 | U2 FieldBus Control Active |
| (1)0212 | U2 Above Limit |
| (1)0213 | U2 FB SW Bit 11 |
| (1)0214 | U2 FB SW Bit 12 |
| (1)0215 | U2 FB SW Bit 13 |
| (1)0216 | U2 FB SW Bit 14 |
| (1)0217 | U2 Watchdog |

## Input Register Map (read-only)
| Data element number | Data type | Content description |
|-|-|-|
| (3)0001 | Float (32 bit) | U1.1 DC-Link Voltage [V] |
| (3)0003 | Float (32 bit) | U1.1 Total Current [A] |
| (3)0005 | Float (32 bit) | U1.1 Power (import) [W] |
| (3)0007 | Float (32 bit) | U1.1 Active Current [A] |
| (3)0009 | Float (32 bit) | U1.1 Reactive Current [A] |
| (3)0011 | Float (32 bit) | U1.1 Supply Frequency [A] |
| (3)0013 | Float (32 bit) | U1.1 Supply Voltage [V] |
| (3)0015 | Float (32 bit) | U1.1 Line Frequency D7 [Hz] |
| (3)0017 | Float (32 bit) | U1.1 Line Voltage D7 [V] |
| (3)0019 | UINT (16 bit) | U1.1 Fault Word 1 |
| (3)0020 | UINT (16 bit) | U1.1 Fault Word 2 |
| (3)0021 | UINT (16 bit) | U1.1 Warning Word |
| (3)0022 | UINT (16 bit) | U1.1 DIN Status |
| (3)0023 | Float (32 bit) | U1.1 Reactive Power [VAr] |
||||
| (3)0101 ~ (3)0122 | | Reserved for unused U1.2 |
||||
| (3)0201 | Float (32 bit) | U2 DC-Link Voltage [V] |
| (3)0203 | Float (32 bit) | U2 Total Current [A] |
| (3)0205 | Float (32 bit) | U2 Power (import) [W] |
| (3)0207 | Float (32 bit) | U2 Active Current [A] |
| (3)0209 | Float (32 bit) | U2 Reactive Current [A] |
| (3)0211 | Float (32 bit) | ***U2 Supply Frequency [A] |
| (3)0213 | Float (32 bit) | ***U2 Supply Voltage [V] |
| (3)0215 | Float (32 bit) | ***U2 Line Frequency D7 [Hz] |
| (3)0217 | Float (32 bit) | ***U2 Line Voltage D7 [V] |
| (3)0219 | UINT (16 bit) | U2 Fault Word 1 |
| (3)0220 | UINT (16 bit) | U2 Fault Word 2 |
| (3)0221 | UINT (16 bit) | U2 Warning Word |
| (3)0222 | UINT (16 bit) | U2 DIN Status |
| (3)0223 | Float (32 bit) | U2 Reactive Power [VAr] |

****Note: These values are temporarily not available until U2 is equipped with a model 1763.C OPTE9 card*

## Holding Register Map (read/write)
| Data element number | Data type | Content description |
|-|-|-|
| (4)0001 | Float (32 bit) | U1.1 DC-Link Voltage Reference [V] |
| (4)0003 | Float (32 bit) | U1.1 Active Power Reference [W] |
| (4)0005 | Float (32 bit) | U1.1 Reactive Power Reference [VAr] |
| (4)0007 | Float (32 bit) | U1.1 Current Limit [A] |
| (4)0009 | Float (32 bit) | U1.1 Output Active Current Limit [A] |
| (4)0011 | Float (32 bit) | U1.1 Input Active Current Limit [A] |
| (4)0013 | Float (32 bit) | U1.1 Output Power Limit [W] |
| (4)0015 | Float (32 bit) | U1.1 Input Power Limit [W] |
||||
| (4)0101 ~ (4)0115 | | Reserved for unused U1.2 |
||||
| (4)0201 | Float (32 bit) | U2 DC-Link Voltage Reference [V] |
| (4)0203 | Float (32 bit) | U2 Active Power Reference [W] |
| (4)0205 | Float (32 bit) | U2 Reactive Power Reference [VAr] |
| (4)0207 | Float (32 bit) | U2 Current Limit [A] |
| (4)0209 | Float (32 bit) | U2 Output Active Current Limit [A] |
| (4)0211 | Float (32 bit) | U2 Input Active Current Limit [A] |
| (4)0213 | Float (32 bit) | U2 Output Power Limit [W] |
| (4)0215 | Float (32 bit) | U2 Input Power Limit [W] |
||||
| (4)1001 | Float (32 bit) | Test 1 High Active Power Target [W] |
| (4)1003 | Float (32 bit) | Test 1 Low Active Power Target [W] |
| (4)1005 | UINT (16 bit) | Test 1 Ramp Time [s] |
||||
| (4)1101 | Float (32 bit) | Test 2 High Reactive Power Target [VAr] |
| (4)1103 | Float (32 bit) | Test 2 Low Reactive Power Target [VAr] |
| (4)1105 | UINT (16 bit) | Test 2 Ramp Time [s] |
||||
| (4)1201 | Float (32 bit) | Test 3 High Reactive Power Target [VAr] |
| (4)1203 | Float (32 bit) | Test 3 Low Reactive Power Target [VAr] |
| (4)1205 | UINT (16 bit) | Test 3 Ramp Time [s] |

*Note: The FX5U does not retain the values written to holding registers and coils when it is reset or rebooted. They will be initialized with (proper) default values.*