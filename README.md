# CMOS INVERTER Design and Analysis using tsmc 180nm

## Description 
The aim of this project is to help users learn how to use the LTspice tool and understand how a CMOS inverter works. It uses the TSMC180nm model file and starts by studying the basic behavior of MOSFETs. The goal is to look at different plots and find important values related to MOSFETs. After that, the project focuses on the CMOS inverter, where users observe its working and get important plots and values related to its performance.

## MOSFET Model Analysis

### NMOS Analysis
In this part, I begin by analyzing the MOSFET models from the TSMC180nm file. We use Vdd = 1.8V and L = 180nm. For digital circuits, the length is usually taken as the minimum value, and the width is taken around 2 times the length or more. First, I am plotting the Id vs Vgs curve. Below is the LTspice setup used for this.
