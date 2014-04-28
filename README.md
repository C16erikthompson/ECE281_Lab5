ECE281_Lab5
===========

#Part 1

Part 1 involved understanding how a PRISM table appears a waveform.  The table in question appears below:

![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5_table.png?raw=true)

  From viewing the table, it can be seen that this program loads in the value 8 to the accumulator, adds one, then outputs the value in the accumulator to output port 3.  It continues to loop back to the adding operation, printing out the numbers from 9 to F, until ending in an infinite loop.  The following pictures of waveforms, split into 10 ns intervals, show the PRISM table's execution.
  
![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5wave_1.png?raw=true)

  First, the program Fetchs the instruction 7 from the data, then the Decode deciphers this command as LDAI.  Because the command is LDAI, the program does an Immediate Execute, and then returns to Fetch instruction 6 from the data.

![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5wave_2.png?raw=true)

  Here, the Decode deciphes this command as ADDI.  Because the command is ADDI, the program does an Immediate Execute, and then returns to fetch another command.  The program fetches a 3, which is then Decoded to be OUT.

![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5wave_3.png?raw=true)

  To reach the out command, the program passes through Decode LoAddr, which send the "3" through MARLo and then to Direct IO executen performing the out command.  The program then Fetches another command, retrieving a "b" which is decoded to be the JN command.

![](https://github.com/C16erikthompson/ECE281_Lab5/blob/master/Lab5wave_4.png?raw=true)

  To execute the JN command, the program passes through Decode LoAddr, Decode HiAddr (and thus MARLo and MARHi), and performs the Jump execute command if the value stored in the accumulator is less than zero.  If the jump is executed (as it is in this waveform), then the program will jump back to address 02, which perform the ADDI function.  The next part of the waveform shows the program fetching a value of "6" which will then be decoded as ADDI.
  
