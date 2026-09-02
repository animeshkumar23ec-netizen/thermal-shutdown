PVT-ROBUST CMOS THERMAL SHUTDOWN CIRCUIT

Overview

This project presents the design and PVT characterization of a CMOS thermal shutdown circuit implemented using Cadence Virtuoso and Spectre.

The circuit monitors a temperature-dependent sensing voltage and compares it with a reference voltage to detect an over-temperature condition. When the temperature exceeds the defined threshold, the circuit generates a shutdown signal to protect the system from excessive temperature.

The design focuses on reliable temperature detection, low-complexity bias generation, startup reliability, comparator operation, and reduced sensitivity to process, voltage, and temperature variations.

Key Specifications

| Parameter                             | Target / Result                 |
| ------------------------------------- | ------------------------------- |
| Thermal trip temperature              | Approximately 120°C             |
| Recovery temperature                  | Approximately 140°C             |
| Temperature sensing                   | PTAT-based                      |
| Reference                             | CTAT / fixed reference          |
| Comparator                            | Continuous-time CMOS comparator |
| Biasing                               | Constant-gm bias circuit        |
| Startup                               | Dedicated startup circuit       |
| PVT characterization                  | Performed                       |
| Worst-case trip-temperature variation | Approximately 20°C              |

System Architecture

The overall thermal shutdown architecture consists of the following blocks:

Startup Circuit
|
v
Constant-gm Biasing
|
+--------------------+
|                    |
v                    v
PTAT Temperature        Comparator
Sensing Voltage             ^
|                   |
v                   |
Temperature-dependent       |
Voltage Vc                  |
|
CTAT / Reference Voltage Vref
|
v
Thermal Shutdown
Output

Operating Principle

The circuit uses the temperature dependence of semiconductor devices to generate a temperature-dependent sensing voltage.

The PTAT sensing voltage increases with temperature, while the reference voltage provides a comparison level.

At low temperature:

Vc < Vref

The comparator remains in its normal state and the thermal shutdown signal remains inactive.

As temperature increases:

Vc approaches Vref

When the sensing voltage crosses the reference level, the comparator changes state and activates the thermal shutdown signal.

Therefore, the thermal shutdown condition is determined by the crossing between the temperature-dependent sensing voltage and the reference voltage.

Startup Circuit

The constant-gm bias circuit can have a zero-current operating point during power-up if no startup mechanism is provided.

A dedicated startup circuit is therefore included to inject current during the initial supply ramp.

The startup circuit forces the bias network away from the undesired zero-current state and allows the constant-gm circuit to reach its intended operating point.

Once the bias circuit starts operating normally, the startup path becomes inactive.

Constant-gm Biasing

A constant-gm bias circuit is used to generate a relatively stable bias current for the analog blocks.

The generated bias is used to establish the operating point of the PTAT sensing circuit and comparator.

Using a common bias source also provides better tracking between different circuit blocks across process and temperature variations.

The comparator bias is derived from the constant-gm bias network while its transistor sizing can be independently optimized for the required comparator current and response speed.

PTAT Temperature Sensor

The temperature sensing circuit generates a voltage with positive temperature dependence.

The resulting voltage can be represented conceptually as:

Vc increases as temperature increases

Therefore:

dVc/dT > 0

This PTAT characteristic allows the circuit to convert temperature variation into a voltage-domain signal that can be processed by the comparator.

CTAT / Reference Voltage

A reference voltage is generated to establish the thermal detection threshold.

The reference provides the comparison level for the PTAT sensing voltage.

The thermal trip point is determined by the intersection of:

Vc(T) and Vref(T)

By properly selecting the sensing and reference characteristics, the desired thermal trip temperature can be established.

Comparator

A CMOS comparator is used to compare the temperature-dependent sensing voltage with the reference voltage.

The comparator receives:

Input 1: PTAT sensing voltage Vc

Input 2: Reference voltage Vref

The comparator changes its output state when the sensing voltage crosses the reference level.

The comparator bias is derived from the constant-gm bias network. Its transistor sizing can be independently adjusted to control the available current, transconductance, and switching speed without completely changing the bias-generation architecture.

Thermal Hysteresis

The design incorporates separate conditions for thermal shutdown and recovery.

During increasing temperature, the circuit is designed to activate thermal shutdown at approximately:

120°C

During decreasing temperature, the circuit is designed to recover at approximately:

140°C

This creates a temperature window between the shutdown and recovery conditions.

The reference-control network uses MOS switches and a resistor ladder to modify the effective reference condition depending on the operating state.

This prevents unwanted rapid switching when the temperature is close to the thermal threshold.

Simulation Methodology

The circuit was designed and simulated using Cadence Virtuoso with Spectre.

The following analyses were performed:

1. DC operating-point analysis

Used to verify transistor operating regions and bias currents.

2. Temperature sweep

The circuit was simulated across temperature to verify the PTAT sensing behavior and thermal trip point.

3. Transient analysis

Used to verify startup behavior, comparator response, and shutdown operation.

4. PVT analysis

Process, voltage, and temperature variations were evaluated to determine the robustness of the thermal detection circuit.

5. Corner analysis

Different process corners and supply conditions were evaluated to identify the worst-case thermal trip behavior.

Temperature Sensing Result

The PTAT sensing voltage shows a positive temperature coefficient.

As temperature increases, the sensing voltage increases and eventually crosses the reference voltage.

The crossing point determines the thermal shutdown temperature.

Suggested plot:

Temperature vs PTAT sensing voltage

Add your Cadence simulation figure here.

![PTAT Voltage vs Temperature](images/ptat_vs_temperature.png)

Thermal Trip Point

The nominal design targets a thermal shutdown temperature of approximately 120°C.

At the thermal trip point:

Vc ≈ Vref

The comparator detects this crossing and changes its output state, activating the thermal shutdown signal.

Thermal Recovery

When the temperature decreases, the sensing voltage moves back toward its normal operating region.

The reference-control network provides a different effective threshold for recovery.

The circuit is designed to recover at approximately 140°C.

Therefore, the thermal shutdown and recovery points are separated by approximately 20°C.

PVT Characterization

PVT simulations were performed to evaluate the effect of:

Process variation

Supply voltage variation

Temperature variation

The objective was to determine whether the thermal trip point remains within an acceptable range under different operating conditions.

The simulations showed a maximum trip-temperature variation of approximately 20°C across the evaluated PVT conditions.

PVT Trip-Point Behavior

The trip temperature is affected by variations in:

Transistor threshold voltage

Mobility

Bias current

PTAT slope

Reference voltage

Comparator offset

Supply voltage

Process corner

The observed PVT variation was reduced through optimization of the biasing, reference generation, comparator sizing, and switching network.

Design Challenges

The main design challenges encountered during the project were:

1. Zero-current startup condition

The self-biased constant-gm circuit could remain in an undesired zero-current state during startup.

Solution:

A dedicated startup circuit was added to initiate the bias current during power-up.

2. Comparator trip-point variation

The comparator showed different trip temperatures under different PVT corners.

The initial PVT simulations showed a larger variation in thermal trip temperature.

The circuit was optimized to reduce this sensitivity, achieving approximately 20°C worst-case trip-temperature variation in the evaluated simulations.

3. Comparator response

Increasing comparator current can improve transconductance and switching speed.

However, comparator current alone does not fundamentally determine the thermal trip temperature.

The trip point is primarily influenced by the voltage difference between the PTAT sensing signal and reference, together with comparator offset and PVT-dependent bias variations.

4. Thermal shutdown and recovery

A single threshold can result in undesirable switching when the temperature is close to the trip point.

A resistor-ladder-based reference control with MOS switching was used to provide different effective thresholds for shutdown and recovery.

Key Engineering Insights

The project provided practical experience in analog CMOS design and verification.

Important design insights include:

* A self-biased circuit requires a reliable startup mechanism.
* PTAT circuits can be used to convert temperature variation into a measurable voltage.
* Comparator offset can significantly affect thermal trip accuracy.
* Increasing comparator current primarily improves speed and does not necessarily correct a large trip-point error.
* Comparator transistor sizing can be independently optimized while maintaining a common bias reference.
* PVT analysis is essential for evaluating the reliability of analog thermal protection circuits.
* Thermal shutdown and recovery thresholds can be controlled using switched reference networks.
* Device sizing, bias current, and reference generation must be considered together during thermal trip-point optimization.

Tools and Technologies

Cadence Virtuoso

Cadence Spectre

Analog CMOS Circuit Design

PVT Analysis

DC Analysis

Transient Analysis

Temperature Sweep

Comparator Design

PTAT Circuit Design

CTAT Reference Design

Constant-gm Biasing

Startup Circuit Design

CMOS Analog Design

Project Outcome

A CMOS thermal shutdown circuit was designed and characterized for temperature-dependent protection.

The design incorporates:

* PTAT temperature sensing
* CTAT/reference generation
* Constant-gm biasing
* Dedicated startup circuit
* CMOS comparator
* Switched resistor-ladder reference control
* Thermal shutdown and recovery functionality
* PVT characterization

The simulated circuit achieves a nominal thermal shutdown point of approximately 120°C and a recovery point of approximately 140°C, with approximately 20°C maximum trip-temperature variation across the evaluated PVT conditions.

Conclusion

This project demonstrates the complete design and verification flow of an analog CMOS thermal protection circuit.

The work involved transistor-level circuit design, bias generation, temperature sensing, comparator design, startup implementation, thermal threshold control, transient verification, temperature sweeps, and PVT characterization.

The project provided practical experience in designing analog circuits where device-level variations, bias accuracy, comparator behavior, and temperature dependence directly influence system-level performance.
