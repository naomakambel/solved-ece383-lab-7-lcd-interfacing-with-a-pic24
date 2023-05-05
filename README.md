Download Link: https://assignmentchef.com/product/solved-ece383-lab-7-lcd-interfacing-with-a-pic24
<br>



<em>Goals: The goals of this lab are to introduce students to LCD interfacing with the PIC24.</em>

<h1>1.     Introduction</h1>

Liquid Crystal Displays (LCD) have tremendous popularity among developers and consumers. These devices have been used in a wide variety of electronic products. Versatility and low power consumption are among the most attractive features of LCDs. Industry standard LCDs are controlled by Hitachi’s HD44780 chips. These chips allow output and input of character information to and from the LCD displays. In this lab you will:

<ul>

 <li>Interface a PIC24 microcontroller to a 16×2 (16 characters by 2 lines) LCD via a 4-bit interface</li>

 <li>Output text to LCD</li>

</ul>

Read through the entire lab and scan any supplied files before starting work. The reporting requirements have you verify operations performed by the PIC24 system and corresponding C programs.

<h1>2.     Prelab</h1>

For this lab assignment, all programs should be completed as a pre-lab assignment prior to your assigned lab time. It is also highly recommended that you complete wiring of the system prior to the lab time. Use the footprint of the LCD shown in the manual to route the wires.

<strong>TA check: As soon as you enter lab, show the TA your completed C files.</strong>

<h1>3.     TASK 1: Connecting the LCD to the PIC24 system</h1>

For this task you will construct an LCD interface (4-bit mode) to the basic PIC24 system constructed in previous labs. The LCD module used in this lab is HDM16216L-5-L30S from Hantronix. It allows character output in 2 lines with 16 characters per line. This LCD supports both 4-bit and 8-bit interfaces. The datasheet for this LCD module can be found here: <a href="http://www.hantronix.com/down/16216l5.pdf"> http://www.hantronix.com/down/16216l5.pdf</a><a href="http://www.hantronix.com/down/16216l5.pdf">.</a>

The LCD interface is divided into control lines (E, R/W#, RS), data lines (D7:D0) and power (VDD, VSS, VL, K, A). The 4-bit interface mode used in this lab is used to reduce the number of connections between the PIC24 and LCD module, allowing 4 transfer lines to be used (D7:D4). D3:D0 are unused. Figure 1 shows a PIC24 LCD interface for a HDM16216L-5-L30S standardized around the HD44780 LCD controller. <strong>Additional information on the LCD interface and programming can be found in Chapter 8 of the textbook (pages 302-310)</strong>.

The LCD requires a 5V power supply and ground. Further, if you recall, logic voltage level translation can be accomplished by using the open drain configuration and pull-up resistors. In addition, all “digital only” pins on PIC24 are 5V tolerant. Wire the LCD as follows:

<ul>

 <li>Wire all data connections as shown in Figure 1.</li>

 <li>Pins RB[4:7] on the PIC should be connected to D[4:7] on the LCD module (U2 on the schematic) leaving D[0:3] on the LCD module unconnected. Connect Pins RB[8, 9, and 13] with E, R/W#, RS.</li>

 <li>Lines D[4:7] and E, R/W#, RS should also be pulled up to +5V using resistors.</li>

 <li>V<sub>BB </sub>on the LCD module should be connected to ground (GND).</li>

 <li>V<sub>DD </sub>on the LCD module should be connected to 5V (Power Supply).</li>

 <li>The V<sub>DD </sub>– V<sub>L </sub>voltage difference determines the intensity of the characters displayed on the LCD. V<sub>L </sub>can be connected to the wiper terminal of a thumbwheel potentiometer, with another lead on the potentiometer connected to the V<sub>DD </sub>node and the other connected to ground. In our setup, we will connect V<sub>L </sub>to the ground for maximum intensity.</li>

</ul>

<strong>Figure 1. LCD Interface to Microstick II</strong>

<strong>TA check</strong>: <strong>Show the TA the wired LCD interface to the Microstick. Include a picture (from a cell phone) of the wired LCD interface to the Microstick II in the report. See Figure 2 for an example of fully wired system (note: </strong>

<strong>do not literally follow this example, as the connections shown are not the most efficient and easy to replicate). </strong>

<strong>Figure 2. An example of a wired LCD.</strong>

<h1>4.     TASK 2: Character Output to LCD</h1>

<ul>

 <li>Copy the <em>chap8 </em>files to a suitable directory on your PC hard disk.</li>

 <li>Start MPLAB. Open the project lcd4bit.mcp (note: you must start MPLAB first, then open the project file). Create a new C source file named “output_name.c”. Add this file to the project, and remove the source file “lcd4bit.c” from the project.</li>

 <li>Modify the pin values in the code according to Figure 1.</li>

 <li>Modify the code to use open drain configuration for all pins connected to the LCD and configured as</li>

 <li>outputs (data lines, R/W, etc).</li>

 <li>With “lcd4bit.c” as a reference, create a program that is capable of displaying your first and last name on the LCD screen as well as your email address.

  <ul>

   <li>Write a function that displays your first and last name on the top line of the LCD, moves the cursors to the bottom line (1st position) of the LCD, then writes your email address on the bottom line of the LCD.</li>

   <li>To be fair to those with long names, the characters on the screen should scroll across the display (moving right to left) at a rate of 200 ms. This can be done by taking advantage of the writeLCD function provided in “lcd4bit.c”.</li>

   <li>The HD44780 LCD controller datasheet is a good reference.</li>

  </ul></li>

</ul>

<strong>TA  check</strong>:  <strong>Show  the  TA  the  operation  of  the  output_name<em>.c  </em>program.  Include  your  source  language programs in your lab report. Include a picture (from a cell phone is fine) of the LCD displaying your name.</strong>

<h1>5.     TASK 3: Counter output to LCD</h1>

For this task, you will implement a counter with a visual output to the LCD.

<ul>

 <li>Using the project lcd4bit.mcp as a basis, create a new project named counter_LCD.mcp.</li>

 <li>For this task, you will create a program (counter_LCD.c) that will output an incremental counter to the LCD screen as follows:

  <ul>

   <li>Upon initialization of the program, output a character string “000” to the LCD screen. o When SW1 is pressed and released, the number on the LCD screen should increment by 1.</li>

   <li>Once program counts to “60”, the number of the LCD screen should change back to “000” and begin incrementing again on the press and release of SW1.</li>

   <li>To display the integer output, use the following:</li>

  </ul></li>

</ul>




<strong>char str[3]; </strong>

<strong>sprintf(str,”%.3d”,count); outStringLCD(str); </strong>

o Pressing SW2 should clear the count and change the displayed value back to “000”.

<ul>

 <li>Turn on LED1 when the count reaches “60”. Turn LED1 off when the count resets back to “000”.</li>

</ul>

<strong> </strong>

<strong> </strong>

<strong>An  interrupt  service  routine  should  be  programmed  to  handle  the  state  changes  of  the</strong> <strong>pushbutton. Code from the project <em>button_semaphore.mcp </em>in the chap9 directory should be useful or Lecture 6.</strong>




<strong>TA check: Show the TA the operation of the counter_LCD<em>.c </em>program. Include your source language program in your lab report. Include a picture (from a cell phone) of the LCD displaying your counter values (one picture will suffice).</strong>


