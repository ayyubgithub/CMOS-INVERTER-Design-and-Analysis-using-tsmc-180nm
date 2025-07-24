# CMOS INVERTER Design and Analysis using tsmc 180nm

## Description 
The aim of this project is to help users learn how to use the LTspice tool and understand how a CMOS inverter works. It uses the TSMC180nm model file and starts by studying the basic behavior of MOSFETs. The goal is to look at different plots and find important values related to MOSFETs. After that, the project focuses on the CMOS inverter, where users observe its working and get important plots and values related to its performance.

## MOSFET Model Analysis

### NMOS Analysis
In this part, I begin by analyzing the MOSFET models from the TSMC180nm file. We use Vdd = 1.8V and L = 180nm. For digital circuits, the length is usually taken as the minimum value, and the width is taken around 2 times the length or more. First, I am plotting the Id vs Vgs curve. Below is the LTspice setup used for this.

<img width="1366" height="616" alt="Screenshot (3335)" src="https://github.com/user-attachments/assets/5f1aa7e6-9a9f-47f9-acc2-15e6a08d547a" />

The Id vs Vgs curve is plotted by changing Vgs from 0 to 1.8V for different values of Vds. To do this, we use the commands shown in the LTspice schematic

<img width="1361" height="589" alt="Screenshot (3334)" src="https://github.com/user-attachments/assets/fc4ac5b6-bafc-4b3c-966f-efc24200c491" />

This shows us that the threshold value is between 500mV to 650mV



