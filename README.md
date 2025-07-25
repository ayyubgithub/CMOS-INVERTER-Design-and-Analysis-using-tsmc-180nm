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

Before going ahead, let’s first understand — what is an inverter? In simple words, an inverter is a circuit that does the NOT function, meaning it gives the opposite output of the input. Its performance is measured by things like noise margin and speed. Now, I have designed an inverter in LTspice. Here, the width of the PMOS is taken as 4 times the width of the NMOS. So, I have used W_NMOS = 0.36µm and W_PMOS = 1.44µm. Below is the LTspice schematic of this inverter.

<img width="1366" height="637" alt="Screenshot (3346)" src="https://github.com/user-attachments/assets/d2ace9da-ce94-4ab3-940f-a654076d31b9" />

#### 2.2.1 DC Characteristic of CMOS Inverter

We will now plot the Voltage Transfer Characteristics (VTC) curve of the inverter using DC analysis. In this, we change Vin from 0V to 1.8V and plot both Vin and Vout. For this, we use the command: .dc vin 0 1.8 1m. Below is the resulting waveform.

<img width="1366" height="617" alt="Screenshot (3344)" src="https://github.com/user-attachments/assets/1ce9885e-e715-436d-aac3-830662928fb1" />

From the curve, we can see that Vin equals Vout at 0.903V, which is almost equal to VDD/2. This point is called the switching threshold of an inverter.

From the above picture, we can see that the inverter works in five different regions.

<img width="886" height="517" alt="Screenshot (3348)" src="https://github.com/user-attachments/assets/f248fd4c-8a4c-4f8a-888d-34cf13f866b5" />

#### Region I: 
When the input voltage (Vin) is near 0V, the NMOS is OFF and the PMOS is fully ON. This allows the output (Vout) to stay at a strong HIGH (close to VDD).

#### Region II: 
As Vin increases, the NMOS starts to turn ON while the PMOS is still ON. Both transistors conduct current, and the output voltage begins to drop from HIGH towards a lower value.

#### Region III: 
This is the switching region where both NMOS and PMOS are ON. Vin and Vout are nearly equal here, and the inverter becomes very sensitive to changes. This region defines the switching threshold of the inverter.

#### Region IV: 
When Vin increases further, the NMOS is fully ON and the PMOS starts turning OFF. The output continues to drop and approaches 0V.

#### Region V: 
At high Vin (close to VDD), the NMOS remains ON and the PMOS is completely OFF. This pulls the output to a strong LOW level (close to 0V).

#### 2.2.2 Estimation of Noise Margin

<img width="891" height="546" alt="Screenshot (3351)" src="https://github.com/user-attachments/assets/2027d4b4-9614-4e4e-915f-bdf712c45a7e" />

Let’s understand the important parameters of a CMOS inverter using its VTC curve:

VOH – This is the highest output voltage when the output is logic ‘1’.

VOL – This is the lowest output voltage when the output is logic ‘0’.

VIH – This is the highest input voltage that the inverter still sees as logic ‘0’.

VIL – This is the lowest input voltage that the inverter sees as logic ‘1’.

Vth – This is the threshold voltage or switching point of the inverter. We already found it to be 0.903V from the VTC curve.

These five parameters are very important to understand how well an inverter performs. You can locate all of them on the VTC curve.

Now, by using the condition where d(Vout)/d(Vin) = -1, we can find all these parameters. In LTspice, we first plot Vout, then apply the derivative function d() on it, and use the marker tool to measure the values directly from the graph.

<img width="1366" height="612" alt="Screenshot (3345)" src="https://github.com/user-attachments/assets/8e064370-fe56-4627-8ad0-2ea5aafa98c2" />

From the graph above, we find that VIL = 0.78V and VIH = 1.01V

<img width="1366" height="614" alt="Screenshot (3365)" src="https://github.com/user-attachments/assets/066ac17f-43fb-4b35-9299-bbf88a7e62d2" />

from the graph, we calculated VOL=0.1V and VOH=1.696V.

Next, let’s understand Noise Margins. Noise margins show the range of input voltages where the circuit can still work properly, even if there is some noise. This is very important in digital circuits because they use fixed levels (like 0 and 1 in binary), so we need to know how much noise can be tolerated without causing errors. This is also called Noise Immunity.

There are two types of noise margins in binary systems:

NML (Noise Margin Low) = VIL - VOL

NMH (Noise Margin High) = VOH - VIH

Using our calculated values:

NML = 0.78V - 0.1V = 0.68V

NMH = 1.696V - 1.01V = 0.695V

In our case, the noise margins are very accurate and almost equal. However, in some situations, they may not be the same, especially if the threshold voltage (Vth) is not close to VDD/2.
Here is the summary of our results.

####  Parameter.

      Vth                                 0.903

      VIL                                 0.780

      VIH                                 1.010

      VOL                                 0.100

      VOH                                 1.696


## Credits
This work is also the part of simulation tasks given to us in our VLSI Design and Technology course in the fifth semester and also in LT Spice Lab. 


































