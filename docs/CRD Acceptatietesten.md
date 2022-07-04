# CRD Acceptance tests

# Test 1: Active power transport
U2 (right) operates in 'DC Voltage Control mode' maintaining a set DC bus voltage reference. U1.1 (left) operates in 'Power Control' mode. By varying the active power reference for U1.1 from 0 to max (over time) and subsequently from max to min and returning to 0, U2 will follow while keeping the set DC bus voltage reference. While the active power is being varied, the HMI shall display and record readings from the power meters.

# Test 2: Reactive power control 'left'
U1.1 (left) which is still operating in 'Power Control' mode can accept a varying reactive power reference. Similar to Test 1, but instead of active power the reactive power reference is ramped from 0 to max, then to min and back to 0 while the HMI displays and record the readings from the power meters.

# Test 3: Reactive power control 'right'
U2 (right) still operating in 'DC Voltage Control mode' can also accept a varying reactive power reference. Similar to Test 2, but applied to U2