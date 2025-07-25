# CMOS Inverter Design and Analysis using tsmc 180nm

## Description 
The aim of this project is to help users learn how to use the LTspice tool and understand how a CMOS inverter works. It uses the TSMC180nm model file and starts by studying the basic behavior of MOSFETs. The goal is to look at different plots and find important values related to MOSFETs. After that, the project focuses on the CMOS inverter, where users observe its working and get important plots and values related to its performance.

## 1 MOSFET Model Analysis

### 1.1 NMOS Analysis
In this part, I begin by analyzing the MOSFET models from the TSMC180nm file. We use Vdd = 1.8V and L = 180nm. For digital circuits, the length is usually taken as the minimum value, and the width is taken around 2 times the length or more. First, I am plotting the Id vs Vgs curve. Below is the LTspice setup used for this.

<img width="1366" height="616" alt="Screenshot (3335)" src="https://github.com/user-attachments/assets/5f1aa7e6-9a9f-47f9-acc2-15e6a08d547a" />

The Id vs Vgs curve is plotted by changing Vgs from 0 to 1.8V for different values of Vds. To do this, we use the commands shown in the LTspice schematic.

#### Input Plot (Id vs Vgs)
<img width="1361" height="589" alt="Screenshot (3334)" src="https://github.com/user-attachments/assets/fc4ac5b6-bafc-4b3c-966f-efc24200c491" />

This shows us that the threshold value is between 500mV to 650mV.

Now, I am plotting Id vs vds curve, and here is the LT spice setup for that.

<img width="1366" height="638" alt="Screenshot (3354)" src="https://github.com/user-attachments/assets/b15b6db1-ac6d-4153-aa3c-71e7b5ada084" />

The Id vs Vds curve is plotted by changing Vds from 0 to 1.8V for different values of Vgs. To do this, we use the commands shown in the LTspice schematic.

#### Output Plot (Id vs Vds)
<img width="1366" height="616" alt="Screenshot (3337)" src="https://github.com/user-attachments/assets/e3be2a5b-a430-4f64-9bfc-6527684df1af" />

Now, we will find the threshold voltage (Vtn) for NMOS. Below is the LTspice setup for it.

<img width="1366" height="633" alt="Screenshot (3338)" src="https://github.com/user-attachments/assets/0c08e140-241d-4043-8483-25356a7d32e1" />

Here, we have chosen a suitable value of Vgs (greater than Vtn). Using the SPICE error log, we will find the Vtn value. In this case, the width is taken as 0.36µm. You can open the SPICE error log in LTspice by pressing Ctrl + L to see the Vtn value.

<img width="636" height="513" alt="Screenshot (3339)" src="https://github.com/user-attachments/assets/3f468e90-b112-4407-8f6e-c74f6c395faf" />

## 1.2 STRONG 0 AND WEAK 1
What does this mean? To understand it better, look at the schematic and waveforms shown below.

<img width="1366" height="635" alt="Screenshot (3350)" src="https://github.com/user-attachments/assets/b359c28d-53c7-493b-8aea-589ac5e37b14" />

<img width="1366" height="616" alt="Screenshot (3340)" src="https://github.com/user-attachments/assets/a720ed99-5873-4f36-b520-24f60348387d" />

Here, we see that when a square wave is given to the NMOS input, and the input is LOW (0V), the output becomes HIGH (1.8V). But when the input is HIGH (1.8V), the output is not fully LOW — it stays above 0V. This happens because when Vgs is 1.8V, the NMOS works in the linear region, where it behaves like a resistor controlled by voltage. In this condition, the output forms a voltage divider with the NMOS, so the output voltage depends on the resistance. That's why NMOS can pass a strong 0, but it cannot pass a strong 1.

## 1.3 STRONG 1 AND WEAK 0
look at the schematic and waveforms shown below.

<img width="1357" height="607" alt="Screenshot (3343)" src="https://github.com/user-attachments/assets/8ff8aaee-67cf-4bb7-82a3-ca443681cce5" />

<img width="1366" height="614" alt="Screenshot (3342)" src="https://github.com/user-attachments/assets/75d32e5a-5f28-449d-a430-e1bf98aa0ade" />

Here, we see that when a square wave is given to the input of the PMOS, and the input is HIGH (1.8V), the output becomes LOW (0V). But when the input is LOW (0V), the output does not reach the full HIGH level — it stays below 1.8V. This happens because when Vsg is 1.8V, the PMOS operates in the linear region, where it acts like a voltage-controlled resistor. In this condition, the output is part of a voltage divider with the PMOS resistance, so the output voltage depends on that resistance. That’s why PMOS can pass a strong 1, but not a strong 0.

So, using only NMOS or only PMOS does not work well for making an inverter. Many different designs were tried, but the most effective and popular one is the CMOS circuit, which uses both NMOS and PMOS together.

## 2 CMOS INVERTER

### 2.1 Why Chose CMOS Circuit?
In the last part, we saw that NMOS and PMOS alone can't give both proper HIGH and LOW outputs. But they work well together because they are opposite in behavior. This idea led to combining them in one circuit. PMOS, which gives a strong 1, is placed between VDD and the output. NMOS, which gives a strong 0, is placed between the output and ground. This way, one turns ON when the other is OFF, so they don’t conduct at the same time (or do they?). This setup is called CMOS — short for Complementary Metal Oxide Semiconductor — and the simplest version of this is the CMOS inverter.

<img width="889" height="346" alt="Screenshot (3364)" src="https://github.com/user-attachments/assets/d97cfc01-6747-4c49-adde-4aac68cb003f" />

CMOS circuits are usually made of two parts: the top part is called the pull-up network, and the bottom part is the pull-down network. The pull-up uses PMOS transistors, and the pull-down uses NMOS transistors. The idea is simple — when one turns ON, the other turns OFF. This prevents any direct connection between VDD and GND, and avoids major voltage drops. With this setup, we can easily get both a strong HIGH and a strong LOW output. The pull-up gives a low-resistance path to VDD, and the pull-down gives a low-resistance path to GND.

<img width="890" height="561" alt="Screenshot (3352)" src="https://github.com/user-attachments/assets/125f161a-79d2-4501-909c-01f57c89bc5e" />

### 2.2 CMOS Inverter Design and Analysis using LTspice




















