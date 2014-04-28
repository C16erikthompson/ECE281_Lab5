ECE281_Lab5
===========

#Part 1

Part 1 involved understanding how a PRISM table appears a waveform.  The table in question appears below:

![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5_table.png?raw=true)

  From viewing the table, it can be seen that this program loads in the value 8 to the accumulator, adds one, then outputs the value in the accumulator to output port 3.  It continues to loop back to the adding operation, printing out the numbers from 9 to F, until ending in an infinite loop with the final value displayed.  The following pictures of waveforms, split into 10 ns intervals, show the PRISM table's execution.
  
![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5wave_1.png?raw=true)

  First, the program Fetchs the instruction 7 from the data, then the Decode deciphers this command as LDAI.  Because the command is LDAI, the program does an Immediate Execute, and then returns to Fetch instruction 6 from the data.

![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5wave_2.png?raw=true)

  Here, the Decode deciphes this command as ADDI.  Because the command is ADDI, the program does an Immediate Execute, and then returns to fetch another command.  The program fetches a 3, which is then Decoded to be OUT.

![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5wave_3.png?raw=true)

  To reach the out command, the program passes through Decode LoAddr, which send the "3" through MARLo and then to Direct IO executen performing the out command.  The program then Fetches another command, retrieving a "b" which is decoded to be the JN command.

![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5wave_4.png?raw=true)

  To execute the JN command, the program passes through Decode LoAddr, Decode HiAddr (and thus MARLo and MARHi), and performs the Jump execute command if the value stored in the accumulator is less than zero.  If the jump is executed (as it is in this waveform), then the program will jump back to address 02, which perform the ADDI function.  The next part of the waveform shows the program fetching a value of "6" which will then be decoded as ADDI.
  
  I successfully demonstrated full functionality of this part.
  
#Part 2

  I successfully demonstrated full functionality of this part, to include the "cool" program on the FPGA (rotating counter).

Questions and Answers
---------------------

1.	When the controller’s current state is “FETCH,” what is the status of the following control lines:

a.	PCLd - High

b.	IRLd - High

c.	ACCLd - Low


2.	The current state is Decode LoAddr and the IR contains “OUT.”  What are the control signals are asserted, and what will the next state be?
	
The control signals are MARLoLd and PCld.  Next state is Direct IO Execute

3.	What are the three status signals sent from the PRISM datapath to the PRISM controller?

1, A = 0, A < 0

4.	Why is it important that ACCLd signal be active during the execute state for the ADDI instruction?

ADDI adds the value in the operand to the accumulator, to do so, the value in he accumulator most be known, so it is loaded by the ACCLd signal
	
5.	What changes are necessary to the PRISM datapath to add another instruction (SUBI, which would subtract an immediate value from the accumulator) to the instruction set?

The number of bits for the control signals would need to increase, which in turn would increase the size of addr and the PC.
