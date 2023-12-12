# 4 Bit Cyber Lock
This repo contains the digital circuit that determines the 4-bit password of a system, using an optimized Linear Search Algorithm. 

This can also be considered as a Password Detector. The project aims at presenting a small model of how an actual password hacking system would look like.


## Components Required:


| Name | Specifications     |Quantity|
| :-------- | :------- | :------------------------- |
| D Flip Flop | IC 7474 | 4 |
| Quad 2 Input AND Gate | IC 7408 | 2 |
| Quad 3 Input AND Gate | IC 7411 | 2 |
|Quad 2 Input OR Gate | IC 7432 | 1 |
| Quad 3 Input 3 OR Gate | IC 744075 | 1 |
| LED's | - | 2 |
| 4 Bit Magnitude Comparator | IC 7485 | 1 |
| JK Flip Flop | IC 7476 | 5 |
 | Connecting Wires | - | As Required |


## A look into the Components
### 1. D Flip Flop (IC 7474)
D flip-flop, also known as a data flip-flop or delay flip-flop, is a sequential digital logic circuit that has one data input (D), one clock input (CLK), and one output (Q). The output Q simply follows the input D on the rising edge of the clock CLK. In other words, the D flip-flop stores the value of the data input D until the next rising edge of the clock, at which point it transfers the value of D to the output Q.

![image](https://github.com/sayanbose04/4-Bit-CyberLock/assets/131597521/4e4c0a9f-d45c-488d-ad49-5a3a7b8024f1)

### 2. JK Flip Flop (IC 7485)
JK flip-flop, also known as a J-K flip-flop or toggle flip-flop, is a type of sequential logic circuit that has two data inputs (J and K), one clock input (CLK), and one output (Q). 

![image](https://github.com/sayanbose04/4-Bit-CyberLock/assets/131597521/d1298af9-6b57-4a43-a306-a87a07288320)


### 3  . 	4-Bit Magnitude Comparator (IC 7485)

A 4-bit magnitude comparator is a combinational circuit that compares two 4-bit binary numbers and determines their relative magnitudes. It has two sets of 4-bit inputs, A and B, and three outputs:
#### Greater than (>): This output is high if A is greater than B, and low otherwise.
#### 	Equal to (=): This output is high if A is equal to B, and low otherwise.
####	Less than (<): This output is high if A is less than B, and low otherwise.

![image](https://github.com/sayanbose04/4-Bit-CyberLock/assets/131597521/0d97e684-9bf2-4029-a1f1-5f960a029036)


## Circuit Working

The circuit mainly consists of two parts:
1.	Waveform Generator
2.	Password Detector

   #### 1. Waveform Generator
The special 19-bit sequence is: 0000111100101101000. This sequence can be fed as input using a function generator, the absence of which, a T flip flop and a counter are used to generate the sequence. We may convert a JK flip flop to a T flip flop by providing J=K.

The places at which the sequence change from 0 to 1 or 1 to 0, i.e. toggles are noted. When the counter equals to these place values, the T flip flop must be given HIGH, else it must be LOW. 

Writing the excitation table and simplifying it using K-Map, we get the combinational circuit that must be given to the T flip flop. The output of the T flip flop produces the required sequence which is passed serially to the shift register.



![image](https://github.com/sayanbose04/4-Bit-CyberLock/assets/131597521/bfbeab8c-3ee8-40fd-a3b6-604eac71f9d9)

The 1’s denote the states where bit toggling took place and 0’s denote the states where no toggling took place.


![image](https://github.com/sayanbose04/4-Bit-CyberLock/assets/131597521/522c6189-31ef-4526-869f-ebfe7253da52)


The final expression is:

T= Q1’ Q0’ + Q1 Q2 Q3’ + Q1 Q2’ Q3


#### 2.	Password Detector
This is the primary circuit, which is responsible for tallying each of the 4-Bit combinations with the predefined password in the system, using a 4-Bit magnitude comparator. The speed of the entire circuit is decided by the clock frequency given to the flip flops.

It uses SIPO shift register having a synchronous clock input. The output of the T flip flop is fed to the input of the SIPO shift register. The inputs are then shifted to each of the cascaded flip flops on every clock pulse. The initial stage of the shift register is 0000, and then it starts displaying the different input combinations. Each of the output of the flip flops is given to the magnitude comparator which then compares each bit with the predefined password of the system. As soon as the pattern matches the A=B terminal goes high and the green LED glows which shows the correct password is detected, until then the red LED glows. 

To store the password once it is detected, the clock generated and the output of Red LED are given to an ‘AND’ gate which serves as the clock for the shift register. Once the sequence is matched, red LED goes to 0 and the clock to each shift register is 0 and the password is stored on the Shift Registers.










