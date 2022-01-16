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


# 1. Step 1
## 1.1. Original Paper McPat and which processors were used
<br />
&nbsp;&nbsp;&nbsp;&nbsp;In the document presented McPAT is an integrated power system, area, and timing modeling framework that supports integrated design space exploration for multicore and processor configurations ranging from 90nm to 22nm and beyond. At the microarchitecture level, McPAT includes Models for the fundamental elements of a multiprocessor chip, including on- and off-series processor cores,
on-chip networks, shared caches, embedded memory controllers and multi-region timing. In the circuit and in the technology level, McPAT supports critical path timing modeling, surface modeling, and dynamic power, short circuit, and leakage power modeling for each of the device types provided in the ITRS roadmap, including bulk CMOS, SOI and dual-gate transistors. McPAT has a flexible XML interface for to facilitate its use with multiple performance simulators. <br />
&nbsp;&nbsp;&nbsp;&nbsp;McPAT advances the state of the art in several directions compared to Wattch, which is the current standard for power research. First, McPAT is an integrated power, area, and timing modeling framework that enables architects to use new metrics combining performance with both power and area such as energy-delay-area2 product (EDA2P) and energy-delay-area product (EDAP), which are useful to quantify the cost of new architectural ideas. McPAT specifies the low-level design parameters of regular components (e.g. interconnects, caches, and other array-based structures) based on high-level constraints (clock rate and optimization target) given by a user, ensuring the user is always modeling a reasonable design. This approach enables the user, if they choose, to ignore many of the low-level details of the circuits being modeled. <br />
<br />

The following table shows which processors were originally used in McPat:

| Processor | Published total power and area | McPAT Results | % McPAT error |
| :--------: | :--------------------: | :-------------------: | :-----------: |
|  Niagara  | 63 W / 378 mm2 | 56.17 W / 295 mm2  | -10.84 / -21.8 |
|  Niagara2   | 84 W / 342 mm2 | 69.70 W / 248 mm2 | -17.02 / -27.3 |
| Alpha 21364  | 125 W / 396 mm2 | 97.9 W / 324 mm2 | -21.68 / -18.2 |
| Xeon Tulsa  | 150 W / 435 mm2 | 116.08 W / 362 mm2 | -22.61 / -16.7 |

<br />
