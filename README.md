![image](https://github.com/user-attachments/assets/63bee4a1-7cfa-4f29-ab80-c7b33192504c)

Short description:
It is a storage unit designed for automatic sheet metal processing machine. It has 5 storage positions on vertical, each one with a normal adapter for parts loading/unloading and,  another position from below which has a special adapter used to  transfer parts to the processing machine. This special adapter can be pushed inside to make space for interchanging the parts storage positions.


Hw/Sw:\
CPU: S7-300 / Simatic STEP7 V5.5\
HMI: OP17 / ProTool 6

### Program blocks architecture

![ver1-Blocks_architecture](https://github.com/user-attachments/assets/8f45fb86-d8ea-47d2-972b-ed8f81c98f80)

- OB1 - Runs the main program
- OB82 – monitors the CPU modules status 
- OB100 – runs the blocks, which are called in it, during the CPU startup
- FC54 – OP17 HMI has no memory card for tags values storage, so after a restart all important tag values are transferred to the interface
- FC62 – deals with lifter commands at the electrical motors level
- FC66 – deals with lifter commands at the hydraulic/pneumatic devices level
- FC71 – Converting Gray code into decimal. Gray code is also a binary but is changing one bit at a time for ensuring safety in transmitting information from physical devices. In this case a 11-bit encoder readout, which is hardwired, is used for vertical position:\
  <br/>
		  Graycode bit G11 MSB = Decimal bit B11 MSB, for the rest it is calculated by\
            $$B_i = B_{i+1} \oplus G_i$$ 

- FC57 – Inverter’s control. Electrical circuit is wired in such a way that a single inverter is controlling two motors speed and direction, and this block is managing this switching and the respective commands 
- FC50, FC72 and FC73 – are the blocks for state machine
- FC65, FC69, FC70 – Manages the operator’s HMI functions like:
    - monitoring IO devices 
    - stores information about sheet metal parts, 
    - operator commands and more
- FC61 – Controls the modes of operation like EOCY, MANUAL, AUTOMATIC, START/STOP CYCLE
- FC60, FC55, FC131 – Monitors machine normal running conditions and manages critical faults, warnings and other messages
<br/>

### Program workflow

![ver1-Workflow](https://github.com/user-attachments/assets/e1c0a569-3b7c-4ae9-9f78-5c974135e5f0)
