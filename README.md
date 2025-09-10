# Dominance Fault Collapsing and Parallel Fault Simulation and Deductive Fault Simulation
This project is based on Digital VLSI Testing and Testability. The netlist and input_vector is given as input, the code performs Dominance fault collapsing, Parallel fault simulation, Deductive fault simulation.


# Prerequisite for this project
1) Create a netlist by naming all wires with numbers (increasing order 1,2,3,.....), starting from input to output. example is shown below
2) Save the netlist in .txt format and edit netlist file name in code. (Don't give extra spacing at end of netlist).
3) install plotly Python library. This Python library is used to tabulate simulation result.     ```pip install plotly``` 
4) Change input vectors as needed, numbering of input vector is from increasing order of inputs of the circuit. This input vector is used for both Parallel fault simulation and Dominace fault simulation.

# Example (4:1 MUX netlist is used for simulation)
```
NAND 5 3 4
AND 14 6 7
AND 15 8 9
AND 16 10 11
AND 17 12 13
OR 21 14 15
OR 23 16 17
NAND 24 19 20
AND 25 21 24
AND 26 22 23
OR 27 25 26
INPUT 1 7 9 11 13 18
OUTPUT 27
FANOUT 1 2 8 12
FANOUT 2 3 4
FANOUT 5 6 10
FANOUT 18 19 20 22
```

![mux-01]<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4a85ae81-c9ca-4775-8209-b2efb17f9cd7" />




The code contain many variable and functions which are used in fault collapsing and fault simulation. Each cell in code contain description of variabels and function. 



# Dominance Fault Collapsing
Fault F2 is said to dominate the fault F1 if all tests of fault F1 detect another fault F2. If fault F2 dominates F1, then F2 is removed from the fault list.
To collapse faults of a gate, all faults from the output can be eliminated retaining one type of fault on each input and the other type on any one of the inputs. The collapsing rules are different for different gates (AND,OR,NAND,NOR).
Collapse ratio is better.

The code first initializes fault at each node. 
```sa0_5``` this implies that ```stuck at 0 at node 5```.

Consider fault is present at each node. Then traverse throuth output of circuit to input of circuit and Collapse fault considering rules for dominance fault collapsing.


![DominanceFault-01]<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ddc152e9-7084-4e08-828c-2de10183bce9" />



# Parallel Fault Simulation
Parallel fault simulation most effective, Circuit consists of only logic gates where all gates are assumed to have the same delay. Simulate stuck-at fault using bit-parallelism of logical operations in a digital computer.

The code takes input_vector as input and perform parallel fault simulation and tabulate the simulated output and calculate fault coverage for corresponding input vector.

![pf2]<img width="1948" height="3083" alt="image" src="https://github.com/user-attachments/assets/55cf676e-dcb5-4ac3-9760-7ff259ac34af" />


![pfsr]<img width="1904" height="1904" alt="image" src="https://github.com/user-attachments/assets/dd3cd9b1-c00d-4e3a-a32a-c2517ed4407b" />



# Deductive Fault Simulation
Use gate level model with zero or unit delay and two level signal.
This is One-pass simulation, where each line k contains a list Lk of faults detectable on it. Considering true-value simulation of each vector, fault lists of all gate output lines are updated using set-theoretic rules, signal values, and gate. 

![drf]<img width="1470" height="986" alt="image" src="https://github.com/user-attachments/assets/3e54fc0e-8a77-4362-aec5-2f231bf933bc" />


![df]<img width="1470" height="986" alt="image" src="https://github.com/user-attachments/assets/8c40d1a0-9b26-447e-a7be-0c494739e7f8" />



The code takes input_vector as input and perform deductive fault simulation and tabulate the propagated faults at output node and calculate fault coverage for corresponding input vector.


# Limitations of Code
1) Netlist need to be numbered in ascending order from input to output.
2) The circuit will may/may not work if feedback is given.
3) Works only for AND,OR,NAND,NOR gates. The not gate should be modeled as NAND inverter / NOR inverter.
4) Can't run netlist with more than 2 input gates.


