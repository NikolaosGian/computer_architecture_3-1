<div id="top"></div>

<br />
<div align="center">
  <h1 align="center">Computer Architecture Assignment 3</h1>
  <h3 align="center">Aristotle University of Thessaloniki</h3>
  <h4 align="center">School of Electrical & Computer Engineering</h4>
  <p align="center">
    Contributors: Kyriafinis Vasilis, Nikolaos Giannopoulos
    <br />
    Winter Semester 2021 - 2022
    <br />
    <br />
  </p>
</div>
<br />

- [1. Step 1](#1-step-1)
  - [1.1. Original Paper McPat and which processors were used.](#11-original-paper-mcpat-and-which-processors-were-used)
  - [1.2. Looking at the results that the McPAT output gives you.](#12-looking-at-the-results-that-the-mcpat-output-gives-you)
  - [1.3. A system with different processors.](#13-a-system-with-different-processors)
  - [1.4. Xeon VS ARM A9.](#14-xeon-vs-arm-a9)
- [2. Step 2.](#2-step-2)
  - [2.1. How will you calculate the energy.](#21-how-will-you-calculate-the-energy)
  - [2.2. Graphs.](#22-graphs)
  - [2.3 Your results obtained in relation to the cost function.](#23-your-results-obtained-in-relation-to-the-cost-function)
 - [3. Source.](#3-source)


# 1. Step 1
## 1.1. Original Paper McPat and which processors were used.
<br />
&nbsp;&nbsp;&nbsp;&nbsp;In the document presented McPAT is an integrated power system, area, and timing modeling framework that supports integrated design space exploration for multicore and processor configurations ranging from 90nm to 22nm and beyond. At the microarchitecture level, McPAT includes Models for the fundamental elements of a multiprocessor chip, including on- and off-series processor cores,
on-chip networks, shared caches, embedded memory controllers and multi-region timing. In the circuit and in the technology level, McPAT supports critical path timing modeling, surface modeling, and dynamic power, short circuit, and leakage power modeling for each of the device types provided in the ITRS roadmap, including bulk CMOS, SOI and dual-gate transistors. McPAT has a flexible XML interface for to facilitate its use with multiple performance simulators. <br />
&nbsp;&nbsp;&nbsp;&nbsp;McPAT advances the state of the art in several directions compared to Wattch, which is the current standard for power research. First, McPAT is an integrated power, area, and timing modeling framework that enables architects to use new metrics combining performance with both power and area such as energy-delay-area2 product (EDA2P) and energy-delay-area product (EDAP), which are useful to quantify the cost of new architectural ideas. McPAT specifies the low-level design parameters of regular components (e.g. interconnects, caches, and other array-based structures) based on high-level constraints (clock rate and optimization target) given by a user, ensuring the user is always modeling a reasonable design. This approach enables the user, if they choose, to ignore many of the low-level details of the circuits being modeled. <br />
<br />

The following table shows which processors were originally used in McPat:

| Processor | Published total power and area | McPAT Results | % McPAT error |
| :--------: | :--------------------: | :-------------------: | :-----------: |
|  Niagara  | 63 W / 378 mm^2 | 56.17 W / 295 mm^2  | -10.84 / -21.8 |
|  Niagara2   | 84 W / 342 mm^2 | 69.70 W / 248 mm^2 | -17.02 / -27.3 |
| Alpha 21364  | 125 W / 396 mm^2 | 97.9 W / 324 mm^2 | -21.68 / -18.2 |
| Xeon Tulsa  | 150 W / 435 mm^2 | 116.08 W / 362 mm^2 | -22.61 / -16.7 |

<br />
<br />

## 1.2. Looking at the results that the McPAT output gives you.

### Dynamic Power.
&nbsp;&nbsp;&nbsp;&nbsp;Wattch (Wattch: a framework for architectural-level power analysis and optimizations) is a widely-used processor power estimation tool. Wattch calculates dynamic power dissipation from switching events obtained from an architectural simulation and capacitance models of components of the microarchitecture. For array structures, Wattch uses capacitance models from CACTI, and for the pipeline it uses models from "Complexity-Effective Superscalar Processors".
When modeling out-of-order processors, Wattch uses the synthetic RUU model that is tightly coupled to the SimpleScalar simulator (The simplescalar tool
set, version 2.0). Wattch has enabled the computer architecture research community to explore power-efficient design options, as technology has progressed; however, limitations of Wattch have become apparent. First, Wattch models power without considering timing and area. Second, Wattch only models dynamic power consumption the HotLeakage package (“HotLeakage: A Temperature-Aware Model of Subthreshold and Gate Leakage for Architects") partially addressed this deficiency by adding models for subthreshold leakage. Third, Wattch uses simple linear scaling models based on 0.8μm technology that are inaccurate to make predictions for current and future deep-submicron technology nodes.

### Static Power.
&nbsp;&nbsp;&nbsp;&nbsp;This interface allows both the specification of the static microarchitecture configuration parameters and the passing of dynamic activity statistics generated by the performance simulator. McPAT can also send runtime power dissipation back to the performance simulator through the XML-based interface, so that the performance simulator can react to power (or even temperature) data. This approach makes McPAT very flexible and easily ported to other performance simulators. McPAT runs separately from a simulator and only reads performance statistics from it. Performance simulator overhead is minor – only the possible addition of some performance counters. Since McPAT provides complete hierarchical models from the architecture to the technology level, the XML interface also contains circuit implementation style and technology parameters that are specific to a particular target processor. Examples are array types, crossbar types, and the CMOS technology generation with associated voltage and device types

### Short-Circuit Power.
&nbsp;&nbsp;&nbsp;&nbsp;Switching circuits also dissipate short-circuit power due to a momentary short through the pull-up and pull-down devices. We compute the shortcircuit power using the equations derived in the work by Nose(Analysis and Future Trend of Short-circuit Power) that predicts trends for short-circuit power. If the ratio of the threshold voltage to the supply voltage shrinks, short-circuit power becomes more significant. Short-circuit power is around 10% of the total dynamic power, with fluctuations within 3.1% across all the technology generations. The main reason for the stable short-circuit power is that we use ITRS technology models that have stable Vth to Vdd ratios.

### Leakage Power.
&nbsp;&nbsp;&nbsp;&nbsp;Gate leakage is an important component in 90nm and 65nm technology, being 37.6% of the total leakage power at 65nm technology.
Hi-k metal gate transistors (45nm High-k+Metal Gate Strain-Ehanced Transistors) are introduced at 45nm, which reduces the gate leakage by more than 90%. SOI technology and double gate (DG) devices that are used at 32nm and 22nm technology also help to keep the subthreshold leakage under control.

### Running different programs on the same processor architecture.
&nbsp;&nbsp;&nbsp;&nbsp;All the results will depend on the runtime of the program and the load it will create.But there is also the constant power consumption due to the short circuits and the leakage power of the technology used by the processor, which we consider as "constant power loss".

## 1.3. A system with different processors.
&nbsp;&nbsp;&nbsp;&nbsp;It may be possible for processor B with an energy consumption of 35 watts to be more energy efficient. This can be achieved by having only processor B for heavy processes and by having processor A for processor A, which will be used for a longer period of time than processor B and thus will have a higher power consumption of processor B. Such a device can be a mobile phone, a laptop or even various micro-systems that need batteries. Such systems are very common in everyday life. McPat can't give the results for two different cores of a processor - that could change if he could give us these conclusions if you count each processor differently and not as an overall processor chip.

## 1.4. Xeon VS ARM A9.

&nbsp;&nbsp;&nbsp;&nbsp;By running the exact commands in the `mcpat/mcpat folder`:

      ./mcpat -infile ProcessorDescriptionFiles/Xeon.xml -print_level 2
      ./mcpat -infile ProcessorDescriptionFiles/ARM_A9_2GHz.xml -print_level 2

the results can be found here [Xeon](https://github.com/NikolaosGian/computer_architecture_3/blob/main/question_1_4/print_level_2/Xeon.txt) and [ARM A9](https://github.com/NikolaosGian/computer_architecture_3/blob/main/question_1_4/print_level_2/ARM_A9_2GHZ.txt). As shown in the table below the differences between Xeon VS ARM A9

| Processor | Area | Peak Power | Total Leakage | Peak Dynamic | Subthreshold Leakage | Gate Leakage | Runtime Dynamic | Subthreshold Leakage with power gating |
| :--------: | :--------------------: | :-------------------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: | :-----------: |
| Xeon | 410.507 mm^2 | 134.938 W | 36.8319 W | 98.1063 W | 35.1632 W | 1.66871 W | 72.9199 W| 16.3977 W|
| ARM A9 | 5.39698 mm^2 | 1.74189 W | 0.108687 W | 1.6332 W | 0.0523094 W | 0.0563774 W | 2.96053 W | - |

<br />

&nbsp;&nbsp;&nbsp;&nbsp;First of all, these two processors are of different technology. ` Xeon is 65nm ` I mean ` ARM A9 45nm ` which are very different in `short-circuit` and `leakege power`. Even the purpose of use of each processor is different for example `Xeon is designed for ITRS high performance` and `ARM A9 ITRS low operation power`. So the ARM A9 will always be better in terms of energy efficiency because it is specifically designed for that in relation to the performance offered by the Xeon will always win. That depends on the application for which each processor will be used.
<br/>
# 2. Step 2.
## 2.1. How will you calculate the energy.
&nbsp;&nbsp;&nbsp;&nbsp;The `EDAP` was calculated for each benchmark and processor configuration as the product of the `total power (runtime dynamic + gate leakage + subthreshold leakage)` by the execution time of each benchmark `(sim_seconds)`.The results are presented in the table below to four decimal places. 

| Cases | EDAP-specbzip | EDAP-speclibm | 
| :--------: | :--------------------: | :--------------------: |
| L2_size = 1MB | 0.1230 | 0.2239 |
| L2_size = 4MB | 0.1198 | 0.2256 |
| L2_assoc = 2-way | 0.1212 | 0.2245 |
| L2_assoc = 4-way | 0.1209 | 0.2245 |
| L1i_size = 64kB | 0.1525 | 0.2948 |
| L1i_assoc = 4-way | 0.1252 | 0.2383 |
| L1i_assoc = 8-way | 0.1289 | 0.2460 |
| L1d_size = 32kB | 0.0688 | 0.1328 |
| L1d_size = 128kB | 0.1478 | 0.2835 |
| L1d_assoc = 4-way | 0.0950 | 0.1768 |
| L1d_assoc = 8-way | 0.1031 | 0.1891 |
| cacheline_size = 32B | 0.0860 | 0.2439 |
| cacheline_size = 128B | 0.1504 | 0.2060 |
| cacheline_size = 256B | 0.2995 | 0.3285 |
| cacheline_size = 256k | 0.1724 | 0.3297 |

<br />

## 2.2. Graphs.
&nbsp;&nbsp;&nbsp;&nbsp;The peak power for each case is shown in the following graphs, divided by benchmark. The red line shows the power recorded for the MinorCPU case without any change in its characteristics. <br />

<img src="https://github.com/NikolaosGian/computer_architecture_3/blob/main/graphs/specbzip_graph.PNG"> 
<br />

<img src="https://github.com/NikolaosGian/computer_architecture_3/blob/main/graphs/speclibm_graph.PNG"> <br />

&nbsp;&nbsp;&nbsp;&nbsp;So we see that peak power is only affected by the different choices in cache size, associativity etc. for each processor, and does not vary depending on the computational load of each benchmark. The graphs show that the largest influence on the final peak power is the `cache line size`, with `27.4066 W` for the largest `256 byte` option and `2.3259 W` for the smallest `32 byte` option.

<br />


## 2.3. Your results obtained in relation to the cost function.
&nbsp;&nbsp;&nbsp;&nbsp;McPAT does not do a full transistor-level simulation of the processor circuits as a mixed-signal simulator would do.Another possible source of errors is gem5, as it defaults to only syscall emulation, ignoring any hardware delays and therefore may have run-time errors. In fact, the TimingSimpleCPU model can reduce errors to some extent, as it takes hardware timing into account. The combination of the two programs multiplies the errors in the generated values if no correction is made before the final calculation.

# 3. Source.
[Paper McPAT](https://www.hpl.hp.com/research/mcpat/micro09.pdf) <br />
[Github From Andreas Brokalakis](https://github.com/kingmouf/cmcpat) <br />
