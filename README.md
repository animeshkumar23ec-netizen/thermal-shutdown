PVT-ROBUST CMOS THERMAL SHUTDOWN CIRCUIT

Overview

This project presents the design and PVT characterization of a CMOS thermal shutdown circuit implemented using Cadence Virtuoso and Spectre.

The circuit uses a PTAT temperature-sensing voltage (Vc) and a constant reference voltage (Vref) generated using a resistive ladder. As temperature increases, the PTAT sensing voltage increases and eventually crosses the reference voltage. The comparator detects this crossing and generates the thermal shutdown signal.

The design focuses on reliable temperature detection, startup operation, bias generation, comparator performance, thermal threshold control, and characterization of temperature-trip-point variation across process, voltage, and temperature conditions.

Key Specifications

| Parameter                                | Target / Result                                   |
| ---------------------------------------- | ------------------------------------------------- |
| Nominal thermal trip temperature         | Approximately 132°C                               |
| Recovery temperature                     | Approximately 171°C                               |
| Temperature sensing voltage              | PTAT                                              |
| Reference voltage                        | Approximately constant Vref from resistive ladder |
| Comparator                               | CMOS comparator                                   |
| Biasing                                  | Constant-gm bias circuit                          |
| Startup                                  | Dedicated startup circuit                         |
| PVT characterization                     | Performed                                         |
| Maximum observed trip-temperature spread | Approximately 37°C                                |

Operating Principle

The thermal shutdown circuit uses a PTAT voltage Vc as the temperature-sensing signal.

Vc is the temperature-dependent voltage in the comparison.

As temperature increases:

Vc increases

The reference voltage Vref is generated using a resistive ladder and is designed to remain approximately constant.

The comparator continuously compares Vc with Vref.

At lower temperature:

Vc < Vref

The comparator remains in its normal state.

As temperature increases:

Vc approaches Vref

At the thermal trip point:

Vc ≈ Vref

The comparator changes state and activates the thermal shutdown signal.

Therefore, the thermal trip temperature is determined by the crossing of the PTAT sensing voltage and the reference voltage.

PTAT Temperature Sensing

The temperature sensing circuit generates a voltage Vc with positive temperature dependence.

The PTAT behavior can be represented as:

dVc/dT > 0

Therefore, Vc increases as temperature increases.

The thermal trip temperature is established by the point at which:

Vc(Ttrip) = Vref

Constant Reference Voltage

A resistive ladder is implemented to generate the reference voltage Vref.

The reference voltage is designed to remain approximately constant over the operating temperature range.

The thermal trip point is therefore established by the crossing between the increasing PTAT voltage Vc and the approximately constant Vref.

Comparator Operation

A CMOS comparator compares the PTAT voltage Vc with the constant reference Vref.

For increasing temperature:

Vc < Vref

Normal operation

Vc = Vref

Comparator trip point

Vc > Vref

Thermal shutdown condition

When Vc crosses Vref, the comparator changes its output state and generates the thermal shutdown signal.

Thermal Shutdown and Recovery

The nominal thermal shutdown temperature is approximately 120°C.

A separate recovery condition is provided for decreasing temperature.

The reference network uses MOS switches and a resistor ladder to establish the required reference condition for the recovery operation.

The target recovery temperature is approximately 140°C.

This separation between shutdown and recovery temperatures prevents unwanted rapid switching when the temperature is close to the thermal threshold.

PVT Characterization

PVT simulations were performed to evaluate the effect of process, supply-voltage, and temperature variations on the thermal trip point.

The nominal design targets a thermal trip temperature of approximately 120°C.

However, transistor characteristics, resistor values, bias currents, supply voltage, and comparator offset vary across PVT conditions.

These variations change the relative position of Vc and Vref and consequently shift the temperature at which the comparator trips.

Across the evaluated PVT conditions, the observed thermal trip temperatures exhibited a maximum spread of approximately 37°C.

This 37°C spread represents the difference between the highest and lowest observed trip temperatures across the evaluated PVT conditions.

The result highlights the sensitivity of the thermal trip point to process and supply variations and provides a basis for further optimization of the sensing circuit, reference network, biasing, and comparator.

PVT Trip-Temperature Spread

The thermal trip temperature is not identical for every PVT condition.

For example, one corner may cause the comparator to trip at a lower temperature, while another corner may cause it to trip at a higher temperature.

The observed maximum spread is approximately:

Trip-temperature spread = Ttrip,max − Ttrip,min

≈ 37°C

Therefore, the circuit exhibits approximately 37°C variation in the thermal trip temperature across the evaluated PVT conditions.

This variation can arise from:

* Transistor threshold-voltage variation
* Mobility variation
* Bias-current variation
* PTAT slope variation
* Resistor variation
* Supply-voltage variation
* Comparator offset
* Process-corner effects

The PVT analysis was used to identify these variations and evaluate the robustness of the thermal shutdown decision.

Design Challenges

1. Startup Reliability

The self-biased constant-gm circuit can remain in a zero-current state during startup.

Solution:

A dedicated startup circuit was implemented to initiate the bias current during power-up and allow the constant-gm circuit to reach its intended operating point.

2. PTAT Temperature Sensing

The sensing voltage must have a predictable temperature dependence so that the thermal trip point can be established accurately.

Solution:

A PTAT sensing circuit was implemented to generate Vc, which increases with temperature.

3. Constant Reference Generation

A stable comparison voltage is required to establish the thermal threshold.

Solution:

A resistive ladder was implemented to generate the approximately constant reference voltage Vref.

4. PVT Trip-Point Variation

The comparator trip temperature changes across process and supply conditions.

The evaluated simulations showed a maximum trip-temperature spread of approximately 37°C.

This variation is mainly associated with changes in transistor parameters, resistor values, bias conditions, supply voltage, and comparator offset.

PVT characterization was therefore performed to identify the worst-case thermal operating conditions.

5. Thermal Shutdown and Recovery

The circuit requires separate temperature conditions for shutdown and recovery.

Solution:

A switched resistor-ladder reference network was implemented to provide the required reference conditions for the two operating states.

Key Engineering Insights

* Vc is the PTAT temperature-sensing voltage.
* Vref is generated using a resistive ladder and is designed to remain approximately constant.
* The comparator trips when Vc crosses Vref.
* The thermal trip temperature is determined by the Vc-Vref crossing.
* Comparator offset can shift the actual thermal trip temperature.
* PVT variations can significantly change the trip temperature.
* The evaluated design showed approximately 37°C maximum trip-temperature spread across the tested PVT conditions.
* A dedicated startup circuit is required for reliable startup of the self-biased constant-gm circuit.
* Comparator current primarily influences comparator speed and operating conditions and is not the primary mechanism for setting the thermal threshold.
* PVT characterization is essential for identifying worst-case thermal trip conditions.

Project Outcome

A CMOS thermal shutdown circuit was designed and characterized using a PTAT temperature-sensing voltage and a resistive-ladder-generated approximately constant reference voltage.

The circuit incorporates:

* PTAT temperature sensing
* Constant reference generation using a resistive ladder
* Constant-gm biasing
* Dedicated startup circuit
* CMOS comparator
* Switched reference network
* Thermal shutdown and recovery functionality
* PVT characterization

The nominal design targets a thermal shutdown temperature of approximately 120°C and a recovery temperature of approximately 140°C.

PVT simulations were performed to evaluate the variation of the thermal trip point under different process and supply conditions.

The evaluated simulations showed a maximum trip-temperature spread of approximately 37°C across the tested PVT conditions.

This characterization provides insight into the sensitivity of the thermal shutdown threshold and identifies areas for further optimization, including PTAT slope, reference accuracy, bias stability, comparator offset, and resistor matching.

Conclusion

This project demonstrates the transistor-level design and PVT characterization of a CMOS thermal shutdown circuit.

The thermal detection mechanism is based on comparing a temperature-dependent PTAT voltage Vc with an approximately constant reference voltage Vref generated using a resistive ladder.

As temperature increases, Vc increases and eventually crosses Vref. The comparator detects this crossing and activates the thermal shutdown signal.

The circuit was evaluated for startup behavior, PTAT sensing, reference generation, comparator operation, thermal shutdown and recovery, temperature variation, and PVT performance.

The nominal thermal trip point is approximately 120°C, with a target recovery temperature of approximately 140°C. Across the evaluated PVT conditions, the maximum observed thermal trip-temperature spread was approximately 37°C.
