# <div align="center"> SEL 351S Protective Relay Training Project Proposal
#### <div align="center"> John Pacek, Alexander Bussell, Hadyn Simmons, Travis Mehaffy, Maddux Stone
<div align="center"> Department of Electrical and Computer Engineering <br>
Tennessee Technological University
<div align="left">



## Introduction


Electrical power systems are essential for infrastructure in our modern-day society, and the use of protective relays plays a critical role in limiting damage when electrical faults do occur. Reliable protection against these electrical faults requires extensive testing that verifies that the relay operates as it is supposed to based on its settings, logic, and overall role in the power system \[1\].

This project will design and build a fully functional testing kit for undergraduate students in power with the main objective being to help these students develop a certain degree of confidence that the selected SEL-351S legacy protective relay will operate as intended.

Testing shall address phase and ground/neutral overcurrent protection (ANSI 50/51), automatic reclosing (ANSI 79) \[2\]. The team shall also implement and evaluate a Hot Line Tag (HLT) pushbutton feature that enables high-speed tripping and blocks reclosing attempts. The custom testing set shall combine AC current injection, TRIP and CLOSE output monitoring, and simulated 52A breaker-status feedback to reproduce fault trips, reclose attempts, and final lockout.

The deliverables for this project will include a timing verification spreadsheet, an easy-to-follow operator procedure, and documentation including any testing limitations within the system.

The main stakeholder of the project is Tennessee Technological University's Electrical and Computer Engineering department. Mainly Dr. Jinshun Su, who will be the primary end user of project within the ECE department. Mr. Daniel Wray, Mr. Conard Murray, and Mr. Robert Craven will also serve as resources on providing technical information and background that helps develop our project.

This proposal will cover the following:

- Formulating the Problem – Establishing the problem and project goals
- Background – Reviewing SEL-351S operation, breaker simulation, and commercial relay testing methods.
- Design Planning – Describing the approach to solve the problem.
- Specifications and Constraints – Describing relay study, test development, hardware design, and system integration.
- Project Management – Outlining resources, costs, and the development schedule.
- Measures of Success – Defining timing tolerances, operating-sequence checks, and acceptance criteria.
- Benefits and Broader Implications – Addressing educational value, safety, sustainability, and ethical responsibility.
- References – Listing supporting technical and professional sources.
- Team Contributions – Identifying each member's responsibilities.

## Formulating the Problem

Most electrical engineering students graduate with little to no practical experience. This project will give students experience working with relays used in industry by creating a piece of lab equipment for use here at Tennessee Tech. The project will simulate real-world industry application thanks to input from Mr. Daniel Wray, who will provide the necessary information on how relays are used in power systems. Dr. Su will represent the ECE department at Tennessee Tech and advise the group on the learning outcomes the device needs to provide students, as well as help in constructing the device for ease of use and safety.

The project will feature three main systems. First, it will need a source that can simulate currents that a real relay would experience. This source shall simulate currents from a real power system, including multiple types of fault currents. Second, the relay, which will be a SEL-351S, shall be programmed with two setting "groups" which will meet the requirements provided by Daniel Wray. It shall also have a "Hot Line Tag" function. Third, there will be a system that can read the output from the relay and simulate a circuit breaker opening and closing.

While SEL does make testing equipment which can be used to simulate current and read the output from a relay such as the SEL-4000 \[1\]. These devices are too expensive to be practical for use in a student laboratory. By creating a device that can test the relay, the need for the SEL-4000 \[1\] can be eliminated. Based on the current prices of the SEL-4000 \[1\] and the SEL-351S \[2\], the overall cost could be cut by almost two-thirds since only the SEL-351S will be needed.

## Background

Electrical power systems require protective devices to detect abnormal operating conditions and isolate faults before they cause unnecessary equipment damage or create additional hazards. Protective relays perform an important role in this process by monitoring electrical quantities and determining when operating conditions require protection. When the conditions defined by the relay are satisfied, the relay can issue a trip command to a circuit breaker, allowing the affected portion of the power system to be isolated \[1\].

Modern protective relays combine multiple protection, control, monitoring, and communication functions within a single device. The SEL-351S protective relay selected for this project provides overcurrent protection, programmable logic, input/output contacts, metering, and event reporting \[1\], \[2\]. These capabilities allow the relay to detect fault conditions and provide information that can be used for power system analysis \[1\].

The protection functions relevant to this project include instantaneous and time-overcurrent protection. ANSI 50 instantaneous overcurrent protection operates when the measured current exceeds a specified pickup threshold, while ANSI 51 time-overcurrent protection operates according to a time-current characteristic determined by the applied current and relay settings \[1\]. The project will test the applicable phase and ground/neutral overcurrent elements in two SEL-351S setting groups. For inverse-time elements, expected operating times will be calculated and compared with measured relay operating times at multiple current levels.

This project will demonstrate automatic reclosing through the SEL-351S ANSI 79 function. In an operating power system, some faults may be temporary, allowing a circuit breaker to be closed again shortly after it has been interrupted. The relay can therefore be configured to initiate a sequence involving tripping, breaker opening, reclosing, and additional operations until the programmed sequence is completed \[1\], \[2\]. The training system will recreate this interaction without requiring an actual high-voltage circuit breaker. When the relay issues a trip command, the test system will indicate an "open-breaker" condition and stop current injection. When an allowable closed command is issued, the system will indicate a "closed-breaker" condition and resume the current required by the test.

Hot Line Tag (HLT) is another protection and control function that will be incorporated into the training system. On the SEL-351S, activating the HOT LINE TAG operator control blocks closing and automatic reclosing of the circuit breaker, overriding the normal RECLOSE ENABLED and CLOSE controls \[2\]. For this project, the SEL-351S logic will be modified according to SEL Application Guide AG2009-12 so that HLT also provides high-speed tripping for the applicable fault condition \[3\]. The modified HLT logic will be implemented and verified in both relay setting groups. Testing will verify that closing and automatic reclosing are prevented while HLT is active and that normal protection and reclosing behavior are restored after HLT is removed.

Circuit-breaker status is also required for correct operation of relay control logic. Circuit breakers commonly provide auxiliary contacts that indicate their operating position. The 52A auxiliary contact follows the state of the breaker and is used to indicate that the breaker is in the closed position \[1\]. For this project, an actual high-voltage circuit breaker will be replaced by a circuit-breaker simulation system. When the simulated breaker is closed, the simulator will assert the appropriate 52A input to the SEL-351S. When a relay trip command causes the simulated breaker to open, the 52A input will be de-energized. This feedback allows the SEL-351S to respond to the simulated breaker state as part of the trip and reclosing sequences.

Testing these functions requires the relay to experience electrical and control conditions representative of those encountered in an operating power system. A controlled AC current source will therefore be used to apply currents to the SEL-351S without producing an actual power-system fault. The current levels required for testing will depend on the final relay settings and selected test points. A circuit-breaker simulation system will receive the relay's TRIP and CLOSE commands and return the appropriate breaker-status feedback, including the required 52A status signal. Together, the current-injection and breaker-simulation systems will allow the relay's protection and control behavior to be evaluated in a controlled laboratory environment.

The completed system is intended to combine these functions into a reusable educational platform for Tennessee Technological University. Rather than requiring students to interact with an energized distribution system or depend entirely on professional relay-testing equipment, the training system will provide a controlled environment for studying relay configuration, overcurrent protection, circuit-breaker control, automatic reclosing, and protective-relay testing. Test results will allow expected and measured relay behavior to be compared so that students can observe not only whether the relay operates, but also whether it operates according to its programmed protection settings.

## Specifications and Constraints

**Specifications**

The project shall provide a test system for evaluating an SEL-351S legacy protective relay. The following specifications are derived from the stakeholder-provided project instructions.

1. The relay shall be configured and tested in both Normal Group 1 and "Alternative" Group 2 operations.
2. Testing shall verify ANSI 50/51 phase and ground/neutral overcurrent trip timing and operating sequences in both settings groups.
3. Testing shall verify ANSI 79 automatic-reclosing behavior with reclosing enabled and disabled, including the complete programmed sequence from the initial fault to final lockout.
4. An advanced Hot Line Tag function shall be implemented through a relay pushbutton according to SEL Application Guide AG2009-12. When enabled, HLT shall introduce high-speed tripping and block all closing attempts. The applicable logic modifications shall be implemented and verified in both Normal Group 1 and "Alternative" Group 2. HLT shall be disabled during normal operation \[1, pp. 1–3\].
5. A verification spreadsheet shall compare expected and actual protective-element operating times for the applicable relay operating states, as determined by pushbutton statuses and the active settings group. Passing ranges shall be established using the applicable SEL-351S specifications.
6. The test system shall simulate circuit breaker operation and inject AC current within the relay's permissible input limits and at levels sufficient for the required tests. Single-phase injection is permitted, provided its effects on phase and ground inverse-time testing are addressed in the test procedure. SEL publishes separate ratings for standard and sensitive current-input configurations; the installed configuration shall determine the applicable limits \[2\].
7. Trip operating time shall be measured from current-injection onset until the assigned TRIP output asserts. Each tested inverse-time curve shall include at least four test points.
8. Upon a relay trip command, the test system shall stop injecting current and de-energize the relay's 52A input to indicate an open breaker. Upon a relay close command, the system shall assert the 52A input to indicate a closed breaker and then inject the fault current required by the test.
9. The system shall measure and assess repeated trips and closes throughout the complete reclosing sequence.
10. The team shall provide a detailed test procedure suitable for a novice operator and a final test report that automatically assigns pass/fail results, lists deviations, and highlights problematic areas.

**Constraints**

The SEL-351S relay testing system will be designed to operate under the following safety and regulatory requirements:

1. The material cost for the SEL-351S relay test system shall not exceed the approved project budget given by Tennessee Technological University.
2. The test system shall use IEC 61010-1 as a design reference for electrical measurement, control, and laboratory equipment safety. \[3\]
3. The testing system shall comply with any applicable Tennessee Technological University laboratory safety policies and faculty supervision requirements. \[4\]
4. The test system shall remain within the voltage, current, contact-loading, and thermal ratings specified for the installed SEL-351S relay and all test-system components. \[5\]
5. The simulated 52A breaker-status voltage shall be compatible with the assigned relay input. \[5\]
6. The test system shall electrically isolate low-voltage control and measurement electronics from hazardous-voltage circuits. \[3\]
7. The test system shall incorporate guarded terminals, appropriate grounding, and overcurrent protection. \[3\], \[6\]
8. Design and testing shall prevent hazards or disruption to students, faculty, laboratory equipment, and nearby electrical systems. \[4\], \[6\]
9. The test system shall conform to additional client, faculty, and campus requirements established before laboratory use.

## Survey of Existing Solutions

Existing approaches to protective-relay education and testing include manufacturer training, educational laboratory systems, circuit breaker simulators, professional relay-testing equipment, and power-system simulation software. The solutions reviewed below address relay familiarity, practical testing experience, and distribution-system coordination.

Schweitzer Engineering Laboratories (SEL) offers several training courses covering the SEL-351 family, including the SEL-351S. These courses provide instruction ranging from introductory operation to hands-on testing and troubleshooting. **CBT 351: Introduction to SEL-351 Relays** is a four-hour, self-paced course covering SEL-351 and SEL-351S protection functions, front and rear-panel interfaces, settings, logic programming, communications, and event reporting. Its learning activities include simulated front-panel operation, interpreting indicators, configuring inputs and outputs, and entering settings through acSELerator QuickSet software. The course also covers retrieving event data and using metering and sequential event records to diagnose problems \[1\]. **APP 351: SEL-351 Protection System** provides application training for the SEL-351 family. Its published course information includes distinctions among SEL-351 models, SEL-351S operator controls, breaker monitoring, and use of acSELerator QuickSet. Hands-on exercises are included in the course agenda \[2\]. **TST 103: SEL Feeder Relay Testing** is a three-day course focused on entering settings, testing, commissioning, and troubleshooting SEL relays. The course uses several relay models, including the SEL-351S, and includes hands-on SEL-351S testing and analysis. Learning outcomes include calculating test points from relay settings, interpreting relay logic, and analyzing responses through metering, sequential event recording, and event reports \[3\].

An educational laboratory system includes Festo Didactic's numerical-relay instructional modules based on Siemens SIPROTEC equipment. Its LabVolt Series 3813 numerical distance relay is described as a training system based on the SIPROTEC 5 series. These products represent an existing approach to teaching numerical protection using commercial relay technology in an educational setting \[4\]. Festo Didactic also has the LabVolt Series 3812-A Numerical Directional Overcurrent Relay which is designed for studying overcurrent, overload, and directional protection. This equipment represents an approach to teaching protective-relay operation through a dedicated instructional module \[5\].

Some standalone circuit breaker simulators could be the **Barrington Model CBS**, which is designed to verify protective-relay trip and close operation without operating a high-voltage circuit breaker. It accepts trip and close commands and provides six auxiliary contacts: three normally open and three normally closed. The simulator also includes manual trip and close buttons, LED indications, and protection against reverse polarity or incorrectly applied source volage. Barrington specifies operation with 48 VDC and 125 VDC systems \[6\]. **The PONOVO PSS01** is another commercial circuit breaker simulator. It simulates breaker tripping and closing and returns feedback during secondary protection-scheme testing. PONOVO describes the device as an accessory used alongside a relay test set and states that it can operate with relay testers from other manufacturers. Its purpose is to support testing of the secondary protection circuit while avoiding repeated operation of the actual breaker \[7\].

For professional relay-testing equipment, the OMICRON CMC 500 is a modular, multiphase test system designed to evaluate protective relays and protection systems. It supports testing applications ranging from electromechanical relays to digital protection devices. With OMICRON's Test Universe software, it supports detailed testing of individual relay functions; with RelaySimTest, it supports evaluation of protection-system behavior under simulated network conditions \[8\]. This test system can range between \$60,000 - \$120,000, depending on the package and software options selected. \[9\]

A directly relevant publication is "_Designing and Testing Protective Overcurrent Relay Using Real Time Digital Simulation,"_ by A. Saran, P. Kankanala, A. K. Srivastava, and N. N. Schulz, presented in 2008. The Real Time Digital Simulator (RTDS) hosted abstract describes Hardware in the Loop (HIL) testing of a physical SEL-351S overcurrent relay within an eight-bus power-system model. It also describes the development of a software relay model in RSCAD and a proposed procedure for software-in-the-loop testing \[10\].

## Measures of Success

The success of the project will be determined by testing the completed training system under the operating conditions specified for the SEL-351S relay. The testing process shall verify the operation of the current-injection system, SEL-351S protection functions, Hot Line Tag (HLT) logic, circuit-breaker simulation, and data-recording functions. The SEL-351S instruction manual identifies relay testing as a process for verifying protection elements, logic functions, input and output operation, and auxiliary equipment. It also identifies relay metering, event reports, and Sequential Events Recorder (SER) data as tools for evaluating relay performance \[1\].

1. The current-injection system shall be capable of applying the current levels required to test the programmed SEL-351S protection elements. The system shall simulate the fault conditions required by the project without requiring an actual power-system fault. The required current levels shall be determined from the final relay settings for the two setting groups. Testing shall verify that the relay detects currents above the programmed pickup levels and does not produce an unintended trip when the applied current is below the applicable pickup level \[1\], \[2\].
2. Both SEL-351S setting groups shall be tested to verify that the relay operates according to their intended settings. Testing shall include the applicable phase and ground/neutral overcurrent protection functions, including ANSI 50 instantaneous overcurrent and ANSI 51 time-overcurrent elements. For each protection element, the applied current, expected operation, actual operation, and operating time shall be recorded and compared. A test shall be considered successful when the measured relay response falls within the acceptable operating range established by the relay specifications and project requirements \[1\], \[2\].
3. The inverse-time characteristics of the ANSI 51 elements shall be verified. At least four test points shall be used for each applicable inverse-time curve so that the system demonstrates the relationship between fault-current magnitude and relay operating time. The expected operating time at each test point shall be calculated from the relay settings and compared with the measured operating time. This testing methodology is consistent with the testing procedure provided by the project supervisor and the SEL-351S documentation \[1\], \[2\].
4. The ANSI 79 reclosing function shall be tested as a complete sequence rather than only verifying an individual trip or close operation. When reclosing is enabled, the system shall verify that a fault causes the expected trip, breaker opening, reclose attempt, and subsequent trip/reclose operations until the programmed lockout condition is reached. The sequence shall also be tested with reclosing disabled to verify that the relay does not perform an unintended reclose operation \[1\], \[2\].
5. The modified Hot Line Tag (HLT) function shall be verified. When HLT is active, the system shall demonstrate that the relay provides the intended high-speed trip response for the applicable fault condition and prevents the breaker from closing or automatically reclosing. SEL documentation describes HLT as a condition that can block closing and reclosing and provides application guidance for modifying the SEL-351S logic to enable instantaneous tripping during an HLT condition \[3\]. The HLT tests shall also verify that normal protection and reclosing behavior are restored when HLT is removed.
6. The circuit-breaker simulator shall correctly respond to relay trip and close commands. A relay TRIP output shall cause the simulated breaker to indicate an open or de-energized condition, and a relay CLOSE output shall cause the simulator to indicate a closed condition when closing is permitted. The simulated breaker status shall be provided to the relay through the appropriate feedback signal. The test system shall also stop or enable current injection according to the simulated breaker state so that the relay experiences the same basic sequence of events expected from a circuit breaker \[2\].
7. The system shall record sufficient information to determine whether each test passed or failed. Relay event reports, SER information, relay element states, input/output states, applied current, and measured operating time shall be used when applicable to compare expected and actual operation. The SEL-351S documentation identifies event reports and input/output information as methods for determining whether protection elements and auxiliary equipment operate at the correct times \[1\].
8. The completed system shall demonstrate repeatable operation and usability as a training device. Repeated tests performed using the same relay settings and test conditions shall produce consistent results within the established measurement tolerances. A novice user shall also be able to follow the completed test procedure and obtain a clear record of the expected result, measured result, deviation, and pass/fail status without requiring extensive assistance from the project team. The final testing procedure and report shall document the test conditions, expected response, measured response, and any deviations identified during testing.

## Resources

The project will require electrical equipment, protection-relay hardware, test equipment, software, laboratory facilities, and technical guidance. The resources will be selected to allow the completed system to simulate representative power-system faults, operate the SEL-351S relay, simulate circuit-breaker operation, and record the resulting test data.

The primary protection device will be an SEL-351S protective relay. The relay shall be programmed with the two setting groups required by the project and modified to include the required Hot Line Tag functionality. The SEL-351S provides the overcurrent protection, programmable logic, input/output contacts, metering, event reporting, and Sequential Events Recorder functions required for the project \[1\].

A controlled AC current source will be required to simulate the currents that the SEL-351S would experience during normal and fault conditions. The required current output will be determined from the final relay settings and test procedures rather than from a predetermined maximum. Existing OMICRON protection-relay test equipment is available through Tennessee Technological University; it may be used for current injection and relay testing.

The project will also require a circuit-breaker simulation system. This system will include the necessary interface circuitry to receive the SEL-351S TRIP and CLOSE outputs, simulate breaker opening and closing, and return the appropriate breaker-status feedback to the relay. The system shall provide the 52A breaker-status signal required for the relay's control logic. Additional interface components, control relays, power supplies, protection devices, terminal blocks, wiring, and connectors will be required to construct the simulator. The Barrington CBS is a possible candidate for breaker simulation \[1\], \[2\].

A computer will be required for relay configuration, test control, data collection, and documentation. SEL acSELerator QuickSet software will be used as applicable for configuring the SEL-351S, while event and SER information will be used to analyze relay operation \[1\]. Spreadsheet software may be used to calculate expected operating times, compare expected and measured results, and produce pass/fail results. Additional software or automation may be incorporated if it improves the repeatability or usability of the completed training system.

The project will also require laboratory test equipment for construction and verification. Expected equipment includes digital multimeters, oscilloscopes or other timing and measurement equipment as necessary, power supplies, electrical safety equipment, wiring tools, and appropriate protective devices. Existing Tennessee Technological University laboratory equipment will be used whenever practical to reduce project cost.

Technical resources will include the SEL-351S instruction manual, SEL application documentation, relay-testing guidance, and information provided by the project supervisor. The project team will use manufacturer documentation to determine relay settings, operating characteristics, testing methods, and HLT behavior \[1\], \[2\]. Guidance from Daniel Wray will be used to establish the intended relay operating scenarios and test procedures \[3\].

The project will be developed in two major stages. During the current Capstone I semester, the team will focus on relay research, system design, test planning, component selection, and development of the required documentation. During Capstone II, the team will construct the hardware, integrate the relay and breaker simulator, develop the testing procedures, and perform final verification.

## Budget

The project budget is intended to provide a preliminary estimate of the costs required to construct the training system. The estimate is not a detailed bill of materials because the final hardware configuration and availability of existing Tennessee Technological University laboratory equipment have not yet been determined. Existing equipment will be used whenever practical to reduce project cost.

| **Resource**                                            |     | **Estimated Cost**                           |
| ------------------------------------------------------- | --- | -------------------------------------------- |
| SEL-351S relay                                          |     | \$0 if relay donated by SEL.                 |
| OMICRON relay test equipment                            |     | \$0 since laboratory equipment is available. |
| Breaker simulator and interface components              |     | \$200 - \$1,500                              |
| Control relays, terminal blocks, connectors, and wiring |     | \$75 - \$350                                 |
| DC power supplies and protection components             |     | \$0 - \$200                                  |
| Enclosure, mounting hardware, and panel components      |     | \$100 - \$300                                |
| Measurement/data-acquisition hardware                   |     | \$0 - \$300                                  |
| Software                                                |     | \$0 - \$200                                  |
| Miscellaneous prototyping and replacement components    |     | \$50 - \$200                                 |
| Tax 10%                                                 |     | \$43 - \$305                                 |
| Shipping 15%                                            |     | \$64 - \$458                                 |
| **Estimated Total**                                     |     | **\$537 - \$3,813**                          |

The largest uncertainty in the budget is the equipment that is available from the university to be used in the project. One component especially is the equipment used for current injection. The required current output cannot be finalized until the SEL-351S setting groups and test points have been established. Since existing OMICRON relay test equipment is available, a separate current source may not be required. The OMICRON CMC 256-3 (provided through Conard Murray) is designed for protection-relay testing and may be able to provide the controlled current outputs required for relay testing.

If an off-the-shelf solution for the breaker simulator (such as the Barrington CBS) is too costly, then a custom-built breaker simulator must be constructed. The custom breaker-simulator hardware is expected to represent a direct project expense because it will need to be constructed specifically for the training system. Costs will include control relays, interface circuitry, terminal blocks, wiring, connectors, power supplies, protective devices, and an enclosure. The final design will favor commercially available components that can be replaced easily and that allow the system to be reused for future student training \[1\].

Software costs are expected to be limited because the project will use existing Tennessee Technological University resources when available. SEL software and documentation required for configuring and analyzing the SEL-351S will be used as appropriate \[2\]. Existing laboratory measurement equipment will also be used whenever possible.

The proposed budget is therefore intended to establish a reasonable range for project planning rather than represent a final purchase list. The final cost will depend greatly on what equipment is already available to the team through Tennessee Technological University, and which components must be purchased specifically for the custom training system.

## Personnel and Team Skills

Team 5 consists of five Electrical Engineering students with complementary backgrounds in power systems, controls, programming, industrial electrical systems, testing, and engineering analysis. All five members are expected to graduate in Spring 2027. The team has experience spanning academic power-system analysis, industrial electrical equipment, relay systems, PLC programming, engineering testing, data analysis, and technical documentation.

**John Pacek** has interests in power systems and mechatronics, with coursework in power systems, mechatronics, microcomputer systems, and C++ programming. His internship experience includes substantial industrial electrical design and testing work at Arnold Air Force Base. Projects included test-facility power supplies, redundant backup power, a three-phase coolant-pump redesign, and a control-room relay upgrade. He has experience with LTspice, AutoCAD, Excel, industrial relays, three-phase equipment, circuit breakers, electrical panels, and electrical measurements. He also has experience with relay-based control schematics, CAD, technical documentation, project management, and team leadership. He identifies leadership, three-phase power, relay knowledge, physical design, and relay work as areas where he can contribute.

**Alexander Bussell** has a primary interest in power systems and relevant coursework in ECE 3610/4610 Power Systems, ECE 3270 PLC Programming, and C++ programming. His technical background includes C/C++ programming, Python, MATLAB, PLC programming, and experience with Studio 5000 and FactoryTalk. He has hands-on experience with oscilloscopes, DMMs, signal generators, power supplies, current and voltage measurements, motors, three-phase equipment, and soldering. During an internship at a motor shop, he tested multiple AC motors, all of which were three-phase. His reported power-system strengths include advanced AC circuit analysis and three-phase systems, advanced induction-machine knowledge, and intermediate transformer knowledge. He identifies power-system analysis, programming, and research as areas where he can contribute.

**Hadyn Simmons** has a primary interest in power systems and coursework in introductory power systems, power-system analysis, and circuits. His software experience includes MATLAB, LTspice, AutoCAD, and Excel. He reports direct experience working with a substation technician to troubleshoot an electronic recloser and identifies direct experience with SEL relays as his strongest contribution to the project. His power-system background includes intermediate AC circuit analysis, three-phase systems, transformers, circuit breakers, and distribution systems. He also has intermediate C/C++ and Python experience, including a Python crypto-trading-bot project. He is particularly interested in learning relay coordination and relay programming.

**Maddux Stone** has a primary interest in controls. His relevant coursework includes ECE 2140, 3140, 3610, and 3210, with ECE 3610 identified as particularly relevant because of its introduction to basic power distribution. His software experience includes basic MATLAB, intermediate LTspice, and intermediate Excel. His programming background includes intermediate C/C++, basic Python, basic MATLAB, basic VHDL, and PLC Ladder Logic. His strongest programming experience is automating a rotary furnace using PLC Ladder Logic. Maddux identifies troubleshooting and testing as his strongest contributions and is particularly interested in relay programming, fault-detection testing, relay testing, and simulation. His reported power-system knowledge is primarily basic, with no reported experience in protective relays or relay coordination.

**Travis Mehaffy** has a primary interest in power systems and relevant coursework in introductory power systems, power-system analysis, introductory digital systems, and digital-system design. His previous engineering experience includes leading transformer validation testing and data analysis as well as initiating a relay-related geopolitical risk mitigation project. He has experience with MATLAB, LTspice, AutoCAD, Excel, C++, Python, VHDL, Arduino, and Excel VBA. His reported power-system knowledge includes intermediate AC circuit analysis, three-phase systems, per-unit systems, transformers, and circuit breakers, with basic knowledge in several additional power-system areas. Travis is interested in relay function and testing and would like to contribute to development models, physical testing, simulations, data analysis, and project documentation.

Collectively, the team has a broad foundation in power-system analysis, industrial electrical equipment, controls, programming, testing, data analysis, research, and engineering documentation. The team also has several members with direct or related relay experience. At the same time, the questionnaires indicate that hands-on protective-relay testing and relay coordination are areas in which the team will need additional training and sponsor guidance. The team therefore intends to use manufacturer documentation, sponsor-provided training, research, laboratory testing, and guidance from Daniel Wray and the project supervisor to develop the specialized skills required for the project.

**Project Customer**

The project customer will be Tennessee Technological University. Dr. Su, Conard Murray, and Robert Craven will serve as representatives of the customer. Dr. Su will provide academic guidance and serve as the primary academic end user of the project. Conard and Robert will serve as technical resources and advisors, providing background information based on their experience with the most recent attempt to complete this project. They will also provide feedback regarding the project's technical direction and expected outcomes.

**Project Supervisor (Subject-Matter Expert)**

The project supervisor and subject-matter expert will be Daniel Wray. As a Product Sales Engineer for Schweitzer Engineering Laboratories (SEL), he possesses relevant technical expertise in SEL protection relays and their applications. He will provide technical guidance regarding the SEL components and protection-relay aspects of the project and assist the team in resolving project-specific engineering questions. His guidance will help the team ensure that the proposed solution is technically appropriate and consistent with the capabilities and application of the selected protection equipment.

**Instructor**

Dr. Johnson will provide academic oversight, establish course requirements, review project progress, and evaluate the completed project.

## Timeline
<img src= "/Documentation/Gantt Chart.png" width="3200" height="900">



## Specific Implications

Successful completion of the proposed project will provide Tennessee Technological University with a reusable laboratory platform for teaching protective-relay operation and testing. The system will allow students to gain practical experience with an SEL-351S protective relay in a controlled laboratory environment. Students will be able to observe the relationship between simulated fault conditions, relay protection logic, trip and close commands, circuit-breaker status, and recorded relay data. This experience will supplement classroom instruction by allowing power-system protection concepts to be examined through physical testing.

The completed system will allow students to investigate several protection and control functions available on the SEL-351S. Students will be able to test instantaneous and time-overcurrent protection, compare the operation of two relay setting groups, observe automatic-reclosing sequences, operate the Hot Line Tag function, and examine the interaction between the protective relay and simulated circuit breaker \[1\], \[2\], \[3\]. The testing procedure will also require expected relay operating times to be compared with measured operating times. This will allow students to connect calculated protection characteristics and relay settings with the measured response of a physical protective relay.

Another important benefit to Tennessee Technological University will be the repeatability and usability of the completed system. The project will include a detailed test procedure intended for a novice operator as well as a test report that compares expected and actual results, identifies deviations, and assigns pass/fail results. These are already explicit requirements of the proposed system. The system is intended to allow future students to perform established relay tests without requiring extensive assistance from the original project team. This will allow the project to remain useful as an instructional resource after the senior design project is completed.

The proposed system will also make use of existing Tennessee Technological University equipment whenever practical to reduce the amount of equipment that must be purchased specifically for the project. The preliminary project budget estimates a total project cost between \$537 and \$3,813, depending largely on the equipment already available through the university. Existing laboratory equipment may be used for functions such as current injection, measurement, and testing, while project-specific hardware can be constructed for functions such as circuit-breaker simulation. This approach allows project resources to be focused on the equipment necessary to satisfy the intended educational objectives.

The system is also intended to provide value beyond its initial development. Commercially available and replaceable components will be favored where practical so that the system can be maintained, repaired, or modified for future use. This design approach is intended to support continued use of the system for future student training. By combining an industrial protective relay with controlled current injection, circuit-breaker simulation, documented test procedures, and recorded test results, the completed project will provide Tennessee Technological University with both a functional senior design deliverable and a reusable educational tool for instruction in power-system protection.

## Broader Implications, Ethics, and Responsibility as Engineers

The SEL-351S relay test system has implications across global, economic, environmental, and societal contexts. By providing a repeatable method for evaluating protective relay operations, the project can support engineering education and confidence in power-system protection. Responsible implementation requires recognizing potential negative impacts and addressing them through safe design, accurate testing, and transparent reporting. \[5\], \[6\]

1. **Global and Economic Impact**

A fully reusable testing system can reduce the need for students to be dependent on more commercialized lab equipment that may not always be available due to the cost. Giving students hands on experience and the ability to develop knowledge about relays that are used for power system protection throughout the entire world.

1. **Environmental and Societal Impact**

The project having reusable hardware parts helps reduce waste drastically but does produce several potential risks to mitigate.

- Electrical Hazards: Current injection and breaker-status circuits may expose operators to shock, burns, or overheating. Guarded connections, electrical isolation, and overcurrent protection. \[1\], \[3\], \[4\]
- Energy Use and Electronic Waste: Repeated injections consume energy and heat components. Limiting test duration, providing cooling, selecting replaceable parts, and properly recycling electronics shall reduce environmental impact. \[7\]

1. **Ethical Responsibilities**

Each team member will prioritize safety responsibility and honesty throughout the design process. Understanding fully how the system works and all the implications that the system and its results may have. Aligning with the NSPE Code of Ethics for Engineers \[6\].

- Safety: Every member shall follow laboratory procedures, identify hazards, and stop testing when there are unsafe conditions. \[2\], \[4\], \[6\]
- Professional Competence: Team members shall seek faculty/advisor or technical guidance when a task exceeds their knowledge or experience. \[6\]
- Accountability: Each member shall document their work, participate in reviews, and communicate concerns about hardware, settings, logic, or test method. \[5\], \[6\]

## References


**Introduction:**

\[1\] K. Zimmerman and D. Costello, "Lessons learned from commissioning protective relaying systems," Schweitzer Engineering Laboratories, technical paper. Accessed: Oct. 6, 2026. \[Online\]. Available: <https://cdn.selinc.com/assets/Literature/Publications/Technical%20Papers/6360_LessonsLearned_KZ-DC_20120120_Web.pdf>

\[2\] Schweitzer Engineering Laboratories, "SEL-351S protection system," data sheet. Accessed: Oct. 6, 2026. \[Online\]. Available: <https://selinc.com/api/download/5514/?lang=en>

**Formulating the Problem:**

\[1\] SEL. "SEL-4000 Product Page". SEL.com Accessed: Sep. 30, 2026. \[Online.\] Available: <https://selinc.com/products/4000/>

\[2\] SEL. "SEL-351S Product Page". SEL.com Accessed: Sep. 30, 2026. \[Online.\] Available: <https://selinc.com/products/351s/>

**Background:**

\[1\] Schweitzer Engineering Laboratories, Inc., _SEL-351S Relay Instruction Manual_, Date Code 20190809, 2019.

\[2\] Schweitzer Engineering Laboratories, Inc., _SEL-351S Protection System_, Data Sheet. Pullman, WA, USA. \[Online\]. Available: [SEL-351S Protection System Data Sheet](https://selinc.com/api/download/5514/?lang=en&utm_source=chatgpt.com). \[Accessed: Oct. 4, 2026\].

\[3\] D. Costello, K. Behrendt, and A. Amberg, "Enabling instantaneous tripping during a Hot Line Tag condition with the SEL-351S, SEL-351R, and SEL-651R relays," Schweitzer Engineering Laboratories, Application Guide AG2009-12, rev. Jan. 15, 2014.

**Specifications and Constraints:**

\[1\] D. Costello, K. Behrendt, and A. Amberg, "Enabling instantaneous tripping during a Hot Line Tag condition with the SEL-351S, SEL-351R, and SEL-651R relays," Schweitzer Engineering Laboratories, Application Guide AG2009-12, rev. Jan. 15, 2014.

\[2\] Schweitzer Engineering Laboratories, "SEL-351S protection system," data sheet. Accessed: Oct. 1, 2026. \[Online\]. Available: <https://selinc.com/api/download/5514/?lang=en>

\[3\] International Electrotechnical Commission, "Safety requirements for electrical equipment for measurement, control, and laboratory use—Part 1: General requirements," IEC 61010-1:2010+AMD1:2016. Accessed: Oct. 7, 2026. \[Online\]. Available: [https://webstore.iec.ch/en/publication/59769](https://webstore.iec.ch/en/publication/59769?utm_source=chatgpt.com)

\[4\] Tennessee Technological University, "Lab safety." Accessed: Oct. 7, 2026. \[Online\]. Available: [https://www.tntech.edu/safety/lab-safety.php](https://www.tntech.edu/safety/lab-safety.php?utm_source=chatgpt.com)

\[5\] Schweitzer Engineering Laboratories, "SEL-351S protection system," documentation. Accessed: Oct. 7, 2026. \[Online\]. Available: [https://selinc.com/products/351S/docs/](https://selinc.com/products/351S/docs/?utm_source=chatgpt.com)

\[6\] Occupational Safety and Health Administration, "General," 29 CFR 1910.303. Accessed: Oct. 7, 2026. \[Online\]. Available: [https://www.osha.gov/laws-regs/regulations/standardnumber/1910/1910.303](https://www.osha.gov/laws-regs/regulations/standardnumber/1910/1910.303?utm_source=chatgpt.com)

**Survey of Existing Solutions:**

\[1\] Schweitzer Engineering Laboratories, "CBT 351: Introduction to SEL-351 relays." Accessed: Sep. 30, 2026. \[Online\]. Available: [https://selinc.com/selu/courses/cbt/351/](https://selinc.com/selu/courses/cbt/351/?utm_source=chatgpt.com)

\[2\] Schweitzer Engineering Laboratories, "APP 351: SEL-351 protection system." Accessed: Sep. 30, 2026. \[Online\]. Available: [https://selinc.com/selu/courses/app/351/](https://selinc.com/selu/courses/app/351/?utm_source=chatgpt.com)

\[3\] Schweitzer Engineering Laboratories, "TST 103: SEL feeder relay testing." Accessed: Sep. 30, 2026. \[Online\]. Available: [https://selinc.com/selu/courses/tst/103/](https://selinc.com/selu/courses/tst/103/?utm_source=chatgpt.com)

\[4\] Festo, "Numerical distance relay LabVolt Series 3813." Accessed: Sep. 30, 2026. \[Online\]. Available: [https://www.festo.com/in/en/p/numerical-distance-relay-id_PROD_DID_589062](https://www.festo.com/in/en/p/numerical-distance-relay-id_PROD_DID_589062?utm_source=chatgpt.com)

\[5\] Festo, "Numerical directional overcurrent relay LabVolt Series 3812-A." Accessed: Sep. 30, 2026. \[Online\]. Available: [https://www.festo.com/au/en/p/numerical-directional-overcurrent-relay-id_PROD_DID_589110](https://www.festo.com/au/en/p/numerical-directional-overcurrent-relay-id_PROD_DID_589110?utm_source=chatgpt.com)

\[6\] Barrington Consultants, Inc., "CBS." Accessed: Sep. 30, 2026. \[Online\]. Available: [https://www.barringtoninc.com/cbs.htm](https://www.barringtoninc.com/cbs.htm?utm_source=chatgpt.com)

\[7\] PONOVO, "PSS01 circuit breaker simulation device." Accessed: Sep. 30, 2026. \[Online\]. Available: [https://www.ponovo.net/relay-and-protection-testing/optional-accessories/pss01-circuit-breaker-simulator.html](https://www.ponovo.net/relay-and-protection-testing/optional-accessories/pss01-circuit-breaker-simulator.html?utm_source=chatgpt.com)

\[8\] OMICRON electronics, "CMC 500." Accessed: Sep. 30, 2026. \[Online\]. Available: [https://www.omicronenergy.com/en/new-cmc/](https://www.omicronenergy.com/en/new-cmc/?utm_source=chatgpt.com)

\[9\] Eric Foster, "CMC-500 //OMI06920000052," email correspondence to Tennessee Technological University Capstone Team 5, Oct. 2, 2026.

\[10\] A. Saran, P. Kankanala, A. K. Srivastava, and N. N. Schulz, "Designing and testing protective overcurrent relay using real time digital simulation," presented at the Grand Challenges in Modeling & Simulation, Summer Simulation Conference (SummerSim), Edinburgh, Scotland, 2008. Accessed: Sep. 30, 2026. \[Online\]. Available: [https://knowledge.rtds.com/hc/en-us/articles/360048226653-Designing-and-Testing-Protective-Overcurrent-Relay-Using-Real-Time-Digital-Simulation](https://knowledge.rtds.com/hc/en-us/articles/360048226653-Designing-and-Testing-Protective-Overcurrent-Relay-Using-Real-Time-Digital-Simulation?utm_source=chatgpt.com)

**Measures of Success:**

\[1\] Schweitzer Engineering Laboratories, Inc., _SEL-351S Relay Instruction Manual_, Date Code 20190809, 2019.

\[2\] D. E. Wray, "Team 5 Project Summary, Notes, and Tips," email correspondence to Tennessee Technological University Capstone Team 5, Sep. 21, 2026.

\[3\] D. Costello, K. Behrendt, and A. Amberg, "Enabling Instantaneous Tripping During a Hot Line Tag Condition With the SEL-351S, SEL-351R, and SEL-651R Relays," SEL Application Guide AG2009-12, Date Code 20140115, 2014.

**Resources:**

\[1\] Schweitzer Engineering Laboratories, Inc., _SEL-351S Relay Instruction Manual_, Date Code 20190809, 2019.

\[2\] Barrington Instruments, "Model CBS Circuit Breaker Simulator," Barrington Instruments, 2026.

\[3\] D. E. Wray, "Team 5 Project Summary, Notes, and Tips," email correspondence to Tennessee Technological University Capstone Team 5, Sep. 21, 2026.

**Budget:**

\[1\] Barrington Instruments, "Model CBS Circuit Breaker Simulator," Barrington Instruments, 2026.

\[2\] Schweitzer Engineering Laboratories, Inc., _SEL-351S Relay Instruction Manual_, Date Code 20190809, 2019.

**Personnel and Team Skills:** NA

**Timeline:** NA

**Specific Implications:** NA

\[1\] Schweitzer Engineering Laboratories, Inc., _SEL-351S Relay Instruction Manual_, Date Code 20190809, 2019.

\[2\] Schweitzer Engineering Laboratories, Inc., _SEL-351S Protection System_, Data Sheet. Pullman, WA, USA. \[Online\]. Available: [SEL-351S Protection System Data Sheet](https://selinc.com/api/download/5514/?lang=en&utm_source=chatgpt.com). \[Accessed: Oct. 4, 2026\].

\[3\] D. Costello, K. Behrendt, and A. Amberg, "Enabling instantaneous tripping during a Hot Line Tag condition with the SEL-351S, SEL-351R, and SEL-651R relays," Schweitzer Engineering Laboratories, Application Guide AG2009-12, rev. Jan. 15, 2014.

**Broader Implications, Ethics, and Responsibility as Engineers:**

\[1\] International Electrotechnical Commission, "Safety requirements for electrical equipment for measurement, control, and laboratory use—Part 1: General requirements," IEC 61010-1:2010+AMD1:2016. Accessed: Oct. 7, 2026. \[Online\]. Available: [https://webstore.iec.ch/en/publication/59769](https://webstore.iec.ch/en/publication/59769?utm_source=chatgpt.com)

\[2\] Tennessee Technological University, "Lab safety." Accessed: Oct. 7, 2026. \[Online\]. Available: [https://www.tntech.edu/safety/lab-safety.php](https://www.tntech.edu/safety/lab-safety.php?utm_source=chatgpt.com)

\[3\] Occupational Safety and Health Administration, "General," 29 CFR 1910.303. Accessed: Oct. 7, 2026. \[Online\]. Available: [https://www.osha.gov/laws-regs/regulations/standardnumber/1910/1910.303](https://www.osha.gov/laws-regs/regulations/standardnumber/1910/1910.303?utm_source=chatgpt.com)

\[4\] Occupational Safety and Health Administration, "Selection and use of work practices," 29 CFR 1910.333. Accessed: Oct. 7, 2026. \[Online\]. Available: [https://www.osha.gov/laws-regs/regulations/standardnumber/1910/1910.333](https://www.osha.gov/laws-regs/regulations/standardnumber/1910/1910.333?utm_source=chatgpt.com)

\[5\] K. Zimmerman and D. Costello, "Lessons learned from commissioning protective relaying systems," Schweitzer Engineering Laboratories, technical paper. Accessed: Oct. 7, 2026. \[Online\]. Available: <https://cdn.selinc.com/assets/Literature/Publications/Technical%20Papers/6360_LessonsLearned_KZ-DC_20120120_Web.pdf>

\[6\] National Society of Professional Engineers, "Code of ethics for engineers," rev. Jul. 2019. Accessed: Oct. 7, 2026. \[Online\]. Available: [https://www.nspe.org/sites/default/files/resources/pdfs/Ethics/CodeofEthics/NSPECodeofEthicsforEngineers.pdf](https://www.nspe.org/sites/default/files/resources/pdfs/Ethics/CodeofEthics/NSPECodeofEthicsforEngineers.pdf?utm_source=chatgpt.com)

\[7\] U.S. Environmental Protection Agency, "Electronics donation and recycling." Accessed: Oct. 7, 2026. \[Online\]. Available: <https://www.epa.gov/recycle/electronics-donation-and-recycling>

## Statement of Contributions

**John:** John was responsible for the Personnel and Team Skills, Measures of Success, Resources, and Budget sections of the project proposal. He facilitated document section integration and was responsible for document review. He also contributed to researching relay testing, required project resources, and estimated project costs.

**Hadyn:** Hadyn was responsible for the Specifications as part of the Specifications and Constraints section, as well as the Survey of Existing Solutions section. He also contributed to researching relay testing, required project resources, and reaching out to potential companies on quotes for equipment.

**Maddux:** Maddux was responsible for the Background, Specific Implications, and Timeline sections. He also contributed to organizing meetings with stakeholders, researching protective relays, and creating the group's Gantt chart.

**Travis:** Travis was responsible for the introductions, project constraints, and the Broader Implications, Ethics, and Responsibility as Engineer sections. He also contributed to researching protective relays, developing the project's scope, and surveying the existing solutions for the project.

**Alexander:** Alexander was responsible for formulating the problem. He also contributed research on how a current source could be implemented.
