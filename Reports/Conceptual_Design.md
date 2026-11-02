# <div align="center"> SEL 351S Protective Relay Training Conceptual Design
#### <div align="center"> John Pacek, Alexander Bussell, Hadyn Simmons, Travis Mehaffy, Maddux Stone
<div align="center"> Department of Electrical and Computer Engineering <br>
Tennessee Technological University
<div align="left">



## Introduction

Electrical power systems are essential for infrastructure in our modern-day society, and the use of protective relays plays a critical role in limiting damage when electrical faults do occur. Reliable protection against these electrical faults requires extensive testing that verifies that the relay operates as it is supposed to based on its settings, logic, and overall role in the power system [1]. To ensure proper operation, protective relays must undergo testing to verify their response to simulated fault conditions. Commercial relay testing equipment is often expensive, creating a need for more affordable and accessible testing solutions [2].

The Protective Relay Testing System project aims to address this challenge by developing a cost-effective current injection system capable of simulating electrical fault conditions for an SEL-351S protective relay. The proposed system will utilize an STM32 microcontroller, digital-to-analog converter, signal filtering circuitry, and current amplification stages to generate controlled three-phase AC currents [3], [4]. Through a laptop-based interface, users will be able to configure test parameters and select protection functions to evaluate, including ANSI 50 instantaneous overcurrent, ANSI 51 time overcurrent, ANSI 79 automatic reclosing, and Hot Line Tag (HLT) operation [1]. The system is meant to provide a simplified alternative to commercial relay testing equipment while demonstrating protective relay operation and fault simulation for certain conditions.

The primary stakeholders for this project include electrical engineering students, faculty, and laboratory personnel at Tennessee Technological University who would benefit from an accessible testing system for studying and evaluating protective relay behavior. Our team will be responsible for the design, implementation, and validation of the testing system, ensuring that it can generate the required current waveforms and support the evaluation of selected SEL-351S protection functions. By developing a functional and affordable relay testing platform, the project seeks to enhance hands-on learning opportunities and provide a foundation for future improvements in protective relay testing technology.

## Restating the Fully Formulated Problem

The main objective of this project is to develop a current injection test set for the SEL-351S relay. This test set may also be used to fulfill the original project goal of creating a laboratory environment where students can gain hands-on experience working with protective relays. Although commercial relay test sets already exist, they can be extremely expensive and are often more complex to operate than necessary for a university lab course. Therefore, this test set will be designed with safety and ease of use in mind so that it can be operated by novice users with little or no experience working with relays or relay testing equipment.

The test set will be designed to simulate real-world relay operation. The exact test parameters have not yet been established. Daniel Wray, who provided the SEL-351S relay, will supply its configuration settings, which will serve as the basis for the test set's design. Although the specific test requirements are not yet known, the test set is expected to evaluate ANSI functions 50, 51, and 79. It will also test the Hot Line Tag function, which will be programmed into the relay. The maximum peak current for each phase will be limited to 18 A. The provided relay settings will include two operating groups, each of which will determine how the relay responds to fault conditions.

**Constraints and specifications:**
* The test set shall provide a peak amperage of 18 A. (Customer specification)
* The test set shall provide three currents each offset with a phase angle of approximately $120^{\circ}$ from each other. (Customer specification)
* The test set shall not exceed the total budget of $1000 provided by Tennessee Technological University.
* The test set shall remain within the voltage, current, contact-loading, and thermal ratings specified for the installed SEL-351S relay and all test-system components. (Standard)
* The test set shall incorporate guarded terminals, appropriate grounding, and overcurrent protection. [1], [2] (Standard)
* Design and testing shall prevent hazards or disruption to students, faculty, laboratory equipment, and nearby electrical systems. [2], [3] (Ethical concern)
* The test system shall electrically isolate low-voltage control and measurement electronics from hazardous-voltage circuits. [1] (Standard)

## Comparative Analysis of Potential Solutions

Three potential solutions were considered for generating the phase currents required to test the SEL-351S relay: a motor-generator system, an electronic amplifier using two parallel power operational amplifiers per phase, and an electronic amplifier using three parallel power operational amplifiers per phase. Selection factors included waveform control, output-current capability, thermal performance, mechanical complexity, cost, and integration with the test controller.

The first concept involved using a drive motor to rotate a three-phase machine operating as a generator. This arrangement could produce three-phase AC, but would require suitable excitation, speed control, and output conditioning. Independently controlling phase-current magnitudes and angles would require additional circuitry, particularly when reproducing unbalanced faults. Mechanical coupling, rotating components, and maintenance would also increase system complexity. These considerations made the motor-generator approach less suitable for a compact, programmable relay test set.

The second concept used digitally generated waveforms and two parallel power operational amplifiers per phase. An STM32 microcontroller would generate waveform samples, and a DAC would convert them into analog reference signals. The amplifier stages would then regulate the currents injected into the relay. This approach offered direct control of waveform magnitude, frequency, phase angle, and fault duration. However, an output target of 18 A peak would require each amplifier to supply approximately 9-10 A peak under ideal current sharing. For the proposed OPA541AP devices, this would place operation near their stated peak-current capability and leave limited allowance for unequal sharing and current-limit variation.

The selected concept uses three parallel OPA541AP power operational amplifiers in each phase-current channel, for a total of nine power amplifiers. With ideal sharing, an 18 A peak phase current would divide into approximately 6 A peak per amplifier. Compared with the two-amplifier arrangement, this reduces the current contribution required from each device and distributes the power dissipation across more components. The additional devices increase cost, board area, and circuit complexity, but provide greater peak-current margin. [1]

The three-amplifier concept was selected because it combines programmable waveform generation with a more manageable distribution of output current. Appropriate current-sharing circuitry, current feedback, individual current limits, and heatsinking will be required. The stated output capability remains a design target and will be verified through simulation and prototype testing, including evaluation of stability, unequal current sharing, device safe operating area, and temperature rise over the required test distribution.

## High-Level Solution

The high-level solution is a three-channel secondary current-injection test set designed to evaluate the SEL-351S protective relay's response to simulated fault current conditions. The initial design will generate independently controlled phase currents, $I_A$, $I_B$, and $I_C$, to support testing of nondirectional overcurrent protection and selected operating sequences.

Two main DC power sources will supply the system. The relay will receive operating power compatible with its installed power supply option, while an AC/DC conversion stage will provide regulated low voltage power for an STM32 microcontroller, digital-to-analog converter (DAC), and associated control circuitry. The current-amplifier stages will require appropriately rated DC supplies to provide the energy delivered to the relay's current inputs.

The STM32 will digitally generate waveform samples based on selected current magnitudes, frequency, phase angles, and test sequences. Synchronized DAC channels will convert these samples into low-power analog reference signals. Each reference will pass through filtering and signal conditioning circuitry before entering a power operational-amplifier stage configured as a controlled current source. Current feedback will allow each amplifier to regulate the injected current according to its reference signal. The three channels will operate together to reproduce balanced and unbalanced current patterns associated with basic faults.

The initial scope excludes voltage injection and a dedicated neutral-current channel, $I_N$. Testing will therefore focus on functions that can operate using the three phase-current inputs. Ground-overcurrent testing will use residual current calculated from $(I_A+I_B+I_C)$. Testing functions that depend on the separate $I_N$ input would require an additional injection arrangement.

Grounding, electrical isolation, output protection, and other safety provisions remain unresolved design tasks. Detailed design will establish the relationships between control grounds, amplifier returns, relay connections, and protective earth, along with appropriate fault protection and output-disabling measures. These provisions must be resolved and verified before the complete test set is energized and connected to the relay.

## Hardware Block Diagram
*(Placeholder for Hardware Block Diagram)*

## Operational Flow Chart
*(Placeholder for Operational Flow Chart)*

## Atomic Subsystem Specifications

### 1) Safety, Enclosure, Main Power, and AC-to-DC Conversion
This subsystem will create the enclosure for all the test system components. It will ensure proper airflow so that high power components can be cooled. This subsystem will provide both AC and DC power as output to other subsystems. Coordination with other subsystems will be necessary to determine what each subsystem will need. This subsystem will also oversee safety to ensure that users will not be exposed to dangerously high currents. Both the AC and DC power systems will use a standard 120 VAC outlet as input.
* This subsystem shall provide the needed power output to the STM controller and DAC system.
* This subsystem shall provide the needed power output for the amplification subsystem as well.
* The total power supplied shall be more than enough for all subsystems to operate at once.
* This subsystem shall enclose all high voltage and current wires to prevent user injury.
* This subsystem shall design the enclosure with sufficient airflow to cool components and prevent thermal damage.
* Both the AC and DC power systems shall use a standard 120 VAC outlet as input.

### 2) Signal Filtering and Component Wiring:
This subsystem will take the output of the DAC as an input and filter it to ensure that a clean and stable sinewave will be sent, as the system output, to the amplification subsystem and on through the amplification to the relay. It will also support the connection and coordination of the control and amplification subsystems. The coordination of the control and amplification systems includes ensuring that the voltage supplied by the control system reaches the amplification subsystem while accounting for any voltage losses in the DAC, wiring, or filtering.
* This subsystem shall filter out unwanted components of the signals from the controller and DAC.
* This subsystem shall ensure that the signal from the controller is calibrated to the gain of the amplifier so that it is amplified to the appropriate level for each.
* This subsystem shall be responsible for finding and correcting any voltage drops in between the controller and amplification.
* This subsystem shall ensure that all connections within the test system are properly rated for the voltages and currents sent through them.

### 3) STM Microcontroller Control and DAC:
This subsystem will control which tests are being performed by altering the voltage waveforms generated by the STM microcontroller. Multiple tests will need to be performed by the test set. Each test will have a different amplitude but keep the same frequency, and the three phases will be kept $120^{\circ}$ apart so that a real three-phase power system is simulated. The chosen microcontroller will have an internal clock so that all three phases are synchronized.

The DAC will turn the digital waveforms into analog waveforms, which are sent as outputs to the filtering subsystem. This subsystem will need DC power as an input from the power subsystem. There will also be a user interface in the form of either analog or digital buttons that will select the test to run. *(ADD THE FLOWCHART ON GITHUB)*
* This subsystem shall produce three digital waveforms that are synchronized and have matching frequencies.
* The three waveforms shall have phases offset by approximately $120^{\circ}$ as real three-phase power systems do.
* The three waveforms shall have different amplitudes so that after amplification the current output will simulate a real power system fault.
* The digital waveforms shall be converted by the DAC and then output to the filtering subsystem.
* Users shall be able to select from multiple test faults, which will control the change in amplitude of each waveform individually.

### 4) Voltage/Current Amplification:
The voltage waveforms, the microcontroller, and DAC subsystem will have too little power for use of testing the relay, so this subsystem is responsible for amplifying them to the needed power level. Since the waveforms are voltages and not current, this subsystem will also use a 12 high power resistor so that the amplifier output voltage is equal to the output current. The amplifiers will be made using power operational amplifiers. If only one stage of amplification is not enough a low power amplification stage will be added.

The input to this subsystem will be a sinewave from the filtering subsystem and use DC power from the power subsystem as an input which will be used to power the amplifiers. The subsystem will then send current sinewaves to the relay as the system output.
* This subsystem shall amplify the voltage to the needed level for each fault case.
* This subsystem shall not exceed the voltage, current, or power rating of any component.
* This subsystem shall convert the voltage waveforms to current by using a high power resistor.
* This subsystem shall be able to produce the necessary power to create the needed peak current of 18 A.
* This subsystem shall maintain the frequency and phase angles from the filtering stage.
* This subsystem will work with the enclosure subsystem to ensure that no thermal damage is done.

### 5) Relay Programming and Testing:
This subsystem is responsible for interpreting the settings provided for the relay to find the parameters for each test. These parameters will then first be tested by the Omicron CMC-256-3, which will also be used to validate the custom test set by proving it can replicate the function of the CMC-256-3. This subsystem does not have inputs and has an irregular output of the test parameters that will be used by the control subsystem.
* This subsystem shall determine test parameters by analyzing provided relay settings.
* This subsystem shall test the parameters using the CMC-256-3.
* The results from the CMC-256-3 tests shall validate the custom test set by showing it can replicate the results of the CMC-256-3.
* Test parameters determined by this subsystem shall be used by the control subsystem.

## Ethical, Professional, and Standards Considerations

### Broader Impacts
The Protective Relay Testing System has societal and educational implications by supporting hands-on learning about relays that detect electrical faults and help prevent equipment damage and power outages [1]. The accessible testing equipment can strengthen students' understanding of protection systems and reliable electrical infrastructure.

Public health and safety are also a concern because current injection introduces risks from improper wiring, excessive current, and overheating. Electrical protection, current limiting, and thermal management will help protect users and equipment during testing [2].

From an environmental and economic perspective, solid-state electronics and modular components support maintainability and may reduce waste by allowing individual parts to be repaired or replaced. Commercially available components, including the STM32 microcontroller and DAC80504, help the goal of a lower-cost alternative to commercial relay testing equipment for educational laboratories like Tennessee Technological Universities labs.

### Relevant Standards
These standards provide guidance for protective relay operation, electrical safety, and testing procedures:
* **IEEE C37.2 (Device Function Numbers):** Standardizes ANSI 50, 51, and 79 terminology for the testing interface and procedures [3].
* **IEEE C37.90 (Protective Relays):** Provides requirements and test guidance relevant to evaluating protective relay performance and operating responses [3].
* **IEEE 519 (Harmonic Control):** Provides harmonic-control recommendations for electric power systems and reinforces waveform-quality considerations [3].
* **IEC 60255 (Protection Equipment):** Provides requirements and test methods for evaluating relay performance under simulated overcurrent conditions [4].
* **IEC 61010-1 (Laboratory Equipment Safety):** Guides insulation, grounding, enclosures, wiring, and protection against shock and overheating [2].
* **IEC 61000 (Electromagnetic Compatibility):** Provides standards relevant to interference reduction and reliable electronic system operation [4].
* **NFPA 70 (National Electrical Code):** Guides applicable AC connections, wiring, grounding, and overcurrent protection [5].

### Influence on Subsystem Design
The standards and professional responsibilities guide these subsystem choices:
* **Power Supply and Regulation:** IEC 61010-1 and applicable NFPA 70 provisions guide safe isolation, grounding, and protection [2], [5]. The supply must provide stable DC power and support amplifier loads without overheating.
* **Microcontroller and Digital-to-Analog Conversion:** The STM32 and DAC80504 generate three waveforms with controlled timing and phase. IEEE C37.2 guides terminology, while software restricts operation to verified hardware limits.
* **Signal Filtering:** Filters reduce noise and conversion artifacts while preserving waveform amplitude and phase. IEC 61000 guides interference control.
* **Current Amplification:** Each phase targets 18 A peak. Current feedback, protective circuitry, and thermal management support safe operation under IEC 61010-1 principles [2].
* **Protective Relay:** The SEL-351S receives controlled three-phase currents, with ratings, auxiliary power, and settings verified before testing [1]. Relevant IEEE and IEC standards guide evaluation.

## Resources

### Existing Resources
The project team has access to several resources through Tennessee Technological University that will support the development and testing of the relay tester. The SEL-351S protective relay is available for configuration and testing, and the team has access to the OMICRON CMC 256-3 relay test set. The OMICRON unit will provide an established testing platform for comparison and validation of the team's prototype.

The team also has access to a computer and the software necessary for project development, programming, and documentation. University laboratory facilities provide access to some instruments, tools, and prototyping supplies. The availability of specific laboratory equipment and materials will be verified as the project progresses. Dedicated power supplies and certain protection and distribution components are not currently available and will need to be acquired.

### Required Equipment and Materials
The project requires additional electrical and electronic components to construct the prototype. These include power supplies, current amplification components, signal conditioning and filtering components, wiring, connectors, power distribution hardware, and an enclosure. Additional materials will be needed to provide appropriate electrical isolation, grounding, thermal management, and physical protection.

The team will evaluate existing university resources before purchasing additional equipment. Conard Murray may also be able to provide or help obtain certain components and materials through available university resources. Any components obtained through this route will be evaluated for compatibility with the design and accounted for in the project budget as appropriate. Components that cannot be obtained through existing resources will be purchased from approved vendors.

### Personnel and Technical Resources
The project will use the technical knowledge and experience of all five team members. Each member has assigned responsibilities for a portion of the system, including power distribution and enclosure design, signal filtering and wiring, microcontroller and DAC control, current amplification, and relay configuration and testing. Team members will coordinate during subsystem integration and system validation.

The project will also benefit from the guidance and technical support of the faculty advisor, laboratory personnel, and other university contacts.

### Financial Resources and Procurement
The project has a maximum materials budget of $1,000. The team will prioritize the use of existing university resources and any suitable components that may be obtained through Conard Murray before purchasing additional materials. Remaining purchases will be made through approved vendors.

The team will track estimated and actual costs throughout the project to ensure that required components are acquired without exceeding the available budget. Material substitutions and design adjustments may be considered when necessary to maintain the project within its financial constraints.

## Budget

The project has a maximum materials budget of $1,000. The budget is divided according to the five team members' assigned responsibilities to establish the estimated cost of each subsystem and its contribution to the overall project. The baseline design is a three-channel current-injection tester for the SEL-351S protective relay. The optional circuit-breaker simulator is excluded from the baseline budget.

The SEL-351S relay, computer, and software are already available to the team and therefore do not require new purchases. Some laboratory instruments and supplies may also be used. All new purchases will be sourced from approved vendors.

The following costs are planning estimates rather than verified final quotations. Actual costs may be lower due to supplies possibly available from the university. Additional allowances have been included for wiring, connections, filtering components, cooling, and low-voltage power conversion. These allowances must be refined during detailed design.

### John Pacek - Safety, Enclosure, Main Power, and AC-to-DC Conversion
This subsystem provides the main power infrastructure, houses the electronics, and establishes the physical and electrical provisions necessary for safe operation. The estimated costs include the amplifier power supplies, high-current distribution materials, enclosure, mounting hardware, protective grounding materials, and an allowance for low-voltage AC-to-DC conversion for the control circuitry.

| Component | Estimated cost |
| :--- | :--- |
| Two MEAN WELL RSP-500-15, 15 VDC, 500 W power supplies [1] | $195.00 |
| 4 AWG copper wire for main DC power distribution | $25.00-$60.00 |
| 10 AWG stranded copper wire for amplifier power branches | $15.00-$30.00 |
| Covered DC busbar or distribution block | $20.00-$35.00 |
| Crimp lugs and power terminals | $15.00-$30.00 |
| DC fuses and compatible fuse holders | $30.00-$60.00 |
| Hammond RMCV9038BK1 candidate enclosure [2] | $129.54 |
| Screws, nuts, and washers | $10.00-$20.00 |
| Panel-mount connectors and terminals | $15.00-$40.00 |
| Protective grounding hardware and wire | $5.00-$15.00 |
| Wire ties, mounting bases, and sleeving | $5.00-$15.00 |
| Grommets and hole plugs | $3.00-$10.00 |
| Insulating barriers and covers, if required | $5.00-$15.00 |
| Low-voltage AC-to-DC conversion allowance | $20.00-$40.00 |
| **Subsystem total** | **$492.54-$694.54** |

The power supplies provide the proposed amplifier supply rails, while the distribution materials provide the conductors and connections needed to deliver power to the amplifier stages. The enclosure and associated hardware support component mounting, wiring organization, and protection against accidental contact with hazardous parts. The AC-to-DC conversion allowance is provisional; the final implementation will depend on the control circuitry's power requirements and whether an existing source can be used.

The proposed power-supply arrangement, wire ampacity, fuse ratings, grounding, enclosure fit, and ventilation must be verified before construction. The enclosure and supply prices are estimates, and the power-supply arrangement must be checked against manufacturer documentation before procurement.

### Hadyn Simmons - Signal Filtering and Component Wiring
This subsystem conditions the DAC output and coordinates component wiring throughout the system downstream of the main power distribution. The filtering circuitry is intended to reduce unwanted frequency components and improve waveform quality before amplification. Wiring and interconnection materials support the electrical connections between the control, filtering, amplification, and relay-interface stages.

| Component or material | Estimated cost |
| :--- | :--- |
| Filtering resistors, capacitors, and associated components | $10.00-$25.00 |
| Additional interconnection wiring and hookup wire | $15.00-$30.00 |
| Signal connectors, headers, and connection hardware not included elsewhere | $10.00-$20.00 |
| PCB or prototyping materials, if required | $15.00-$30.00 |
| **Subsystem total** | **$50.00-$105.00** |

These costs are allowances pending selection of the filter topology and confirmation of the required wiring quantities. The estimates exclude the high-current power wiring, power-distribution terminals, and panel-mount connectors already budgeted under John's subsystem. They also exclude any amplifier-specific thermal hardware assigned to Alexander's subsystem.

Hadyn will coordinate wiring routes and electrical interfaces with the other subsystem leads. Final wire sizes, insulation ratings, connector ratings, and signal-conditioning components will be selected based on actual current, voltage, frequency, and safety requirements. Any materials available from existing laboratory inventory may reduce these costs after availability is confirmed.

### Travis Mehaffy - STM Microcontroller Control and DAC
This subsystem generates the digital waveform data used to simulate relay fault conditions and converts that data into analog reference signals for the filtering and amplification stages. The proposed implementation uses an STM32 development board and a four-channel digital-to-analog converter.

| Component | Estimated total |
| :--- | :--- |
| STM32 NUCLEO-G474RE development board [3] | $25.49 |
| Texas Instruments DAC80504RTER four-channel DAC [4] | $26.44 |
| **Subsystem total** | **$51.93** |

The listed totals include shipping, which will not be added again. The control board and DAC are proposed components; compatibility with the waveform requirements, communications interface, analog signal ranges, and downstream circuitry must be verified. The low-voltage power-conversion allowance is included under John's subsystem to avoid double-counting.

Development tools and computer resources are already available. The optional circuit-breaker simulator is excluded from the baseline budget and will be considered only if time and remaining funds permit.

### Alexander Bussell - Voltage/Current Amplification
This subsystem amplifies the filtered analog reference signals to produce the controlled current outputs required for relay testing. The proposed component list includes six OPA541AP power operational amplifiers, three high-power resistors, supporting resistors and capacitors, and an additional allowance for amplifier cooling.

| Component | Estimated cost |
| :--- | :--- |
| Nine OPA541AP power operational amplifiers [5] | $296.28 |
| Three HS150 1R J, 1 $\Omega$, 150 W power resistors [6] | $53.40 |
| Supporting low-power resistors | $10.00-$20.00 |
| Capacitors for parallel-operation circuitry | Approximately $5.00 |
| Heat sinks and thermal-management hardware allowance | $40.00-$80.00 |
| **Subsystem total** | **$404.68-$444.68** |

The listed amplifier and resistor prices are estimates and should be confirmed before purchasing. The cooling allowance is provisional because final thermal requirements depend on the amplifier configuration, operating conditions, and physical layout. Amplifier interconnection wiring is assigned to Hadyn's wiring allowance, while the main DC power conductors are included under John's subsystem.

The OPA541's peak current rating does not establish that the proposed arrangement can continuously provide the required output current. Current sharing, safe operating area, dissipation, cooling, and simultaneous operation of all three channels must be validated before the subsystem's capability is established. Additional components identified during that process may require a budget revision.

### Maddux Stone - Relay Programming and Testing
This subsystem covers SEL-351S configuration, test-case development, and verification of relay behavior. Testing will address the required protection functions, operating times, and applicable sequences using the available relay and laboratory resources.

| Resource or expense | Estimated new-purchase cost |
| :--- | :--- |
| SEL-351S protective relay | $0.00 - existing resource |
| Computer and software | $0.00 - existing resources |
| Laboratory instruments and supplies | $0.00 assumed for the current estimate; inventory verification required |
| **Subsystem total** | **$0.00** |

No new purchases have been identified for this subsystem at the conceptual-design stage. The $0.00 estimate does not guarantee that testing will incur no additional cost. Required test leads, adapters, consumables, or other equipment must be added if they are not available in the laboratory. The budget also assumes that no additional paid software is required.

### Consolidated Project Budget
The individual subsystem estimates are combined below to establish the current projected cost of the baseline tester.

| Subsystem lead | Low estimate | High estimate |
| :--- | :--- | :--- |
| John Pacek - Safety, enclosure, power, and AC-to-DC conversion | $492.54 | $694.54 |
| Hadyn Simmons - Filtering and component wiring | $50.00 | $105.00 |
| Travis Mehaffy - STM control and DAC | $51.93 | $51.93 |
| Alexander Bussell - Voltage/current amplification | $404.68 | $444.68 |
| Maddux Stone - Relay programming and testing | $0.00 | $0.00 |
| **Combined estimated subtotal** | **$999.15** | **$1,296.15** |
| Maximum project budget | $1,000.00 | $1,000.00 |
| **Remaining budget (or overrun)** | **$0.85 remaining in budget** | **$296.15 over budget** |

The current estimated cost ranges from $999.15 to $1,296.15. The lower estimate is within the $1,000 materials budget by $0.85, while the upper estimate exceeds the budget by $296.15. The team will need to monitor component costs, verify available laboratory materials, and evaluate possible cost reductions to ensure that the completed system remains within the established budget. The estimates do not consistently include all applicable taxes and shipping costs, so the final purchase total may differ.

### Budget Feasibility and Cost Control
The revised budget indicates that the baseline design may possibly fit within the $1,000 spending limit under the lower cost assumptions, but it is not yet demonstrated to be feasible across the full estimated range. The lower estimate is within the $1,000 materials budget by $0.85, while the upper estimate exceeds the budget by $296.15. Both figures remain provisional because vendor prices, tax, shipping, component quantities, and the final design have not all been verified.

The team will control costs by confirming available laboratory inventory before purchasing additional materials, obtaining current prices from approved vendors, and verifying component specifications before procurement. The optional circuit-breaker simulator will remain outside the baseline budget. The team will also evaluate suitable component alternatives and enclosure options if verified costs exceed the available funds.

The budget will be refined during detailed design as the power arrangement, amplifier capability, filtering requirements, wiring quantities, thermal management, and safety provisions are validated. Any necessary additions must be included in the consolidated budget before procurement. The final design must meet its required functionality and safety constraints without exceeding the $1,000 spending limit.

## Division of Labor

The project team will divide the detailed design into subsystem assignments based on each member's technical background and the functional requirements of the relay test system. John Pacek will serve as the overall project lead, coordinating team activities, monitoring progress, and facilitating communication and integration between subsystem leads. Each member will lead the design of their assigned subsystem, including its specifications, component selection, and interfaces with the rest of the system. All team members will assist across subsystem boundaries when additional expertise or support is needed.

### John Pacek - Overall Project Lead; Safety, Enclosure, Main Power, and AC-DC Conversion
John will coordinate the overall project, facilitate communication between subsystem leads, and oversee system-level integration and progress toward project objectives. He will lead the design of the safety system, enclosure, main power distribution, and AC-to-DC conversion. These responsibilities include electrical isolation, protection against hazardous voltages and currents, wiring organization, safe equipment access, and supplying the power required by the system's electronic and amplification circuits. His experience with industrial electrical design, relays, CAD, schematics, and bills of materials will support these responsibilities.

### Maddux Stone - Relay Programming and Testing
Maddux will lead the development of the SEL-351S relay configuration and testing procedures. This work will include establishing the required relay settings and developing test procedures to verify phase and ground/neutral overcurrent protection, automatic reclosing, and Hot Line Tag functionality. He will help define the expected relay responses and operating times for each test case and compare these expectations with measured results.

### Hadyn Simmons - Signal Filtering and System Wiring
Hadyn will lead the design of the signal-filtering subsystem and coordinate component wiring throughout the project downstream of the main power supply and distribution subsystem. He will design filtering circuitry to reduce unwanted frequency components and improve waveform quality before amplification. He will also organize subsystem interconnections and coordinate with John on power distribution and safety requirements, and with Travis and Alexander on signal connections. His background in power systems, SEL relay experience, and electronic recloser troubleshooting will support these responsibilities.

### Travis Mehaffy - STM Microcontroller Control and DAC; Breaker Simulator (Stretch Goal)
Travis will lead the design and implementation of the STM microcontroller control subsystem and its digital-to-analog converter interface. The microcontroller will generate digital waveform data representing the desired voltage and current test signals. By changing the generated waveform's amplitude, timing, and shape, the system will simulate fault conditions for the SEL-351S relay. The DAC will convert the digital waveform data into an analog signal, which will then pass through the signal-filtering and amplification stages.

As a stretch goal, Travis will also lead the development of a simulated circuit breaker that reproduces breaker opening and closing behavior and provides appropriate breaker-status feedback to the SEL-351S. Work on the breaker simulator will be pursued as time and resources permit after the core project requirements have been addressed.

### Alexander Bussell - Voltage/Current Amplification
Alexander will lead the design of the voltage/current amplification subsystem. Following digital waveform generation, digital-to-analog conversion, and signal filtering, the analog signal will pass through the appropriate amplification stage to reach the voltage or current level required for the selected relay test. The output will then pass through the planned smoothing capacitor stage before being applied to the SEL-351S relay. His experience with AC and three-phase analysis, programming, and industrial automation will support the electrical analysis and implementation of the amplification circuitry. He will coordinate with Travis and Hadyn to ensure that the amplifiers operate correctly with the generated and filtered waveforms.

### Shared Responsibilities
All team members will participate in system integration, troubleshooting, and final validation. Each subsystem lead will document the subsystem's functional requirements, inputs, outputs, component requirements, and design constraints. The team will review the combined design to ensure that the individual subsystems operate together safely and satisfy the project's core requirements. Subsystem leads will remain responsible for their respective designs while incorporating feedback and assistance from the rest of the team.

## Timeline
*(Placeholder for Timeline)*

## References

All sources utilized in the conceptual design that are not considered common knowledge must be properly cited. Multiple references should be included.

### Introduction:
[1] Schweitzer Engineering Laboratories, "SEL-351S Protection System." [Online]. Available: https://selinc.com/products/351S/
[2] OMICRON electronics, "CMC 356-Universal Relay Test Set and Commissioning Tool." [Online]. Available: https://www.omicronenergy.com/en/products/cmc-356/
[3] Texas Instruments, "DAC80504-16-Bit, 4-Channel, SPI Voltage-Output DAC." [Online]. Available: https://www.ti.com/product/DAC80504
[4] Schweitzer Engineering Laboratories, "SEL-351S Protection System Data Sheet." [Online]. Available: https://selinc.com/api/download/5514/?lang=en

### Restating the Fully Formulated Problem:
[1] International Electrotechnical Commission, "Safety requirements for electrical equipment for measurement, control, and laboratory use Part 1: General requirements," IEC 61010-1:2010+AMD1:2016. Accessed: Oct. 7, 2026. [Online]. Available: https://webstore.iec.ch/en/publication/59769
[2] Occupational Safety and Health Administration, "General," 29 CFR 1910.303. Accessed: Oct. 7, 2026. [Online]. Available: https://www.osha.gov/laws-regs/regulations/standardnumber/1910/1910.303
[3] Tennessee Technological University, "Lab safety." Accessed: Oct. 7, 2026. [Online]. Available: https://www.tntech.edu/safety/lab-safety.php

### Comparative Analysis of Potential Solutions:
[1] Texas Instruments, "OPA541AP Power Operational Amplifier," DigiKey. [Online]. Available: https://www.digikey.com/en/products/detail/texas-instruments/OPA541AP/251157. Accessed: Oct. 30, 2026.

### High-Level Solution:
N/A

### Hardware Block Diagram:
N/A

### Operational Flow Chart:
N/A

### Atomic Subsystem Specifications:
N/A

### Ethical, Professional, and Standards Considerations:
[1] Schweitzer Engineering Laboratories, "SEL-351S Protection System." [Online]. Available: https://seline.com/products/351S/
[2] International Electrotechnical Commission, IEC 61010-1: Safety Requirements for Electrical Equipment for Measurement, Control, and Laboratory Use-Part 1: General Requirements. [Online]. Available: https://webstore.iec.ch/
[3] Institute of Electrical and Electronics Engineers, IEEE Standards Collection: Power System Protection and Relaying. [Online]. Available: https://standards.ieee.org/
[4] International Electrotechnical Commission, IEC Standards Collection: Measuring Relays, Protection Equipment, and Electromagnetic Compatibility. [Online]. Available: https://webstore.iec.ch/
[5] National Fire Protection Association, NFPA 70: National Electrical Code. [Online]. Available: https://www.nfpa.org/

### Resources:
N/A

### Budget:
[1] MEAN WELL USA Inc., "RSP-500 Series AC/DC Converters," DigiKey. [Online]. Available: https://www.digikey.com/en/products/base-product/mean-well-usa-inc/1866/RSP-500/461124. Accessed: Oct. 30, 2026.
[2] Hammond Manufacturing, "RMCV9038BK1 Instrument Enclosure," DigiKey. [Online]. Available: https://www.digikey.com/en/products/detail/hammond-manufacturing/RMCV9038BK1/461284. Accessed: Oct. 30, 2026.
[3] STMicroelectronics, "NUCLEO-G474RE Development Board," DigiKey. [Online]. Available: https://www.digikey.com/en/products/detail/stmicroelectronics/NUCLEO-G474RE/10231585. Accessed: Oct. 30, 2026.
[4] Texas Instruments, "DAC80504RTER 16-Bit, Four-Channel Digital-to-Analog Converter." [Online]. Available: https://www.ti.com/product/DAC80504/part-details/DAC80504RTER. Accessed: Oct. 30, 2026.
[5] Texas Instruments, "OPA541AP Power Operational Amplifier," DigiKey. [Online]. Available: https://www.digikey.com/en/products/detail/texas-instruments/OPA541AP/251157. Accessed: Oct. 30, 2026.
[6] Ohmite Manufacturing, "HS150 IR J, 1 $\Omega$, 150 W Chassis Mount Resistor," DigiKey. [Online]. Available: https://www.digikey.com/en/products/detail/ohmite/HS150-1R-J/5307167. Accessed: Oct. 30, 2026.

### Division of Labor:
N/A

### Timeline:
N/A

## Statement of Contributions
Each team member is required to make a meaningful contribution to the project proposal. In this section, each team member is required to document their individual contributions to the report. One team member may not record another member's contributions on their behalf. By submitting, the team certifies that each member's statement of contributions is accurate.

* **John Pacek** - John Pacek contributed to the conceptual design by developing the project budget and resource plan, evaluating required equipment and materials, and organizing team responsibilities. He also led planning for the power distribution, enclosure, and safety subsystems.
* **Travis Mehaffy** - Travis Mehaffy contributed to the conceptual design by writing the introduction and Ethical, Professional, and Standards Considerations. Also led planning for STM Microcontroller Control and DAC subsystem implementation within the testing system.
* **Alexander Bussell** - Alexander Bussell contributed to the conceptual by writing the Restating the Fully Formulated Problem and Atomic Subsystem Specifications sections. Also led planning for the Voltage Amplification subsystem.
* **Maddux Stone** - Maddux Stone contributed to the conceptual design by completing the Timeline, Hardware Block Diagram, and Operational Flow Chart sections. He also led planning for the Relay Programming and Testing subsystem.
* **Hadyn Simmons** - Hadyn Simmons contributed to the conceptual design by completing the Comparative Analysis of Potential Solutions and the High-Level Solution sections. He also helped configure the potential circuitry for the amplifiers.
