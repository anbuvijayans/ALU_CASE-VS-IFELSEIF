# Exp 4 Comparative Study of 32-Bit ALU Implementations Using Case and If-Else Constructs

## Aim: 
Write a Verilog code for 32 32-bit ALU supporting four logical and four arithmetic operations, use case statement and if statement for ALU behavioral modeling. 

To verify the Functionality using Test Bench 

Synthesize and compare the results using if and case statements 

Identify Critical Path and constraints

## Tool Required: 
 Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim) 

 Synthesis: Genus 

## Design Information and Block Diagram: 
The ALU will take in two 32-bit values and a control line. An Arithmetic unit does the following tasks like addition, subtraction, multiplication and logical operations. As the input is given in 32-bit, we get a 32-bit output. The arithmetic will show only one output at a time, so a selector is necessary to select one of the operators. 

 <img width="668" height="344" alt="image" src="https://github.com/user-attachments/assets/b5f95c0d-1fd6-4c3c-9a35-11eb9c86cba3" />

#### Figure No 1: Block Diagram of 32 Bit ALU 

## Creating a Workspace:
Create a folder in your name (Note: Give the folder name without any spaces) and create a new sub-directory named Exp4 or alu_bl_model for the design. Then, open a terminal from the Sub-Directory.

## Creating Source Codes
In the Terminal window, type gedit <filename>.v (ex: gedit alu_case.v).

A Blank Document opens up into which the following source code can be typed.

(Note: File name should be with HDL Extension)

To verify the Functionality using the Test Bench

#### Source Code – Using Case Statement :
```
module alu_case(y,a,b,f); 
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin 
case(f)
3'b000:y=a&b;		//AND Operation
3'b001:y=a|b;		//OR Operation
3'b010:y=~(a&b);	//NAND Operation
3'b011:y=~(a|b);	//NOR Operation
3'b100:y=a^b;    	//XOR Operation
3'b101:y=a+b;		//Addition
3'b110:y=a-b;		//Subtraction
3'b111:y=a*b;		//Multiply 
default:y=32'bx;
endcase
end 
endmodule

```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Creating a Test Bench:
Similarly, create your test bench using gedit <filename_tb>.v to open a new blank document (alu_case_tb.v).

#### Test Bench :
```
module alu_case_tb; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_case dut(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; 
b=32'h00110001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end 
initial
#100 $finish; 
endmodule
```

Use the Save option or Ctrl+S to save the code, or click on the save option from the top-right corner and close the text file.

#### Source Code - Using If Statement :
```
module alu_ifelseif(y,a,b,f);
input [31:0]a;
input [31:0]b;
input [2:0]f; 
output reg [31:0]y; 
always@(*)
begin
if(f==3'b000)
y=a&b;			//AND Operation 
else if (f==3'b001)
y=a|b;	         	//OR Operation
else if (f==3'b010)
y=~(a&b);        	//NAND Operation
else if (f==3'b011)
y=~(a|b);		//NOR Operation
else if (f==3'b100)
y=a^b;			//XOR Operation
else if (f==3'b101)
y=a+b;        		//Addition
 else if (f==3'b110)
y=a-b;			//Subtraction 
else if (f==3'b111)
y=a*b;			//Multiply 
else
y=32'bx; 
end 
endmodule
```

#### Test Bench :
```
module alu_ifelseif_tb; 
reg [31:0]a;
reg [31:0]b;
reg [2:0]f;
wire [31:0]y;
alu_ifelseif dut(.y(y),.a(a),.b(b),.f(f)); 
initial
begin a=32'h00000000; 
b=32'h00110001; 
#10 f=3'b000;
#10 f=3'b001;
#10 f=3'b010;
#10 f=3'b011;
#10 f=3'b100;
#10 f=3'b101;
#10 f=3'b110;
#10 f=3'b111;
end initial
#100 $finish; 
endmodule
```

Functional Simulation for each design

Invoke the cadence environment by typing the commands below

tcsh (Invokes C-Shell)

source /cadence/install/cshrc (mention the path of the tools)

(The path of cshrc could vary depending on the installation destination)

After this, you can see the window like below

To Launch the Simulation tool

•linux:/> nclaunch -new& // “-new” option is used for invoking NCVERILOG for the first time for any design

or

•linux:/> nclaunch& // On subsequent calls to NCVERILOG

It will invoke the nclaunch window for functional simulation. We can compile, elaborate and simulate it using Multiple Steps.

Setting Multi-step simulation

Select Multiple Step and then select “Create cds.lib File” as shown in the figure below

Click the .cds.lib file and save the file by clicking on the Save option

Fcds.lib file Creation

Save .lib file and select the correct option for cds.lib file format based on the HDL Language and Libraries used.

Select “Don’t include any libraries (verilog design)” from “New cds.lib file” and click on “OK” as in the figure below.

We are simulating a verilog design without using any libraries

Click “OK” in the “nclaunch: Open Design Directory” window, as shown in the figure below

![WhatsApp Image 2025-10-30 at 21 08 19_2f2e91be](https://github.com/user-attachments/assets/b605185a-8cd0-4fc9-9c15-f610141e41d8)



#### Fig 2: Selection of Don’t include any libraries
An ‘NCLaunch window’ appears as shown in the figure below

Left side, you can see the HDL files. The right side of the window has Worklib and snapshots directories listed.

Worklib is the directory where all the compiled codes are stored, while Snapshot will have the output of elaboration, which in turn goes for simulation.

To perform the function simulation, the following three steps are involved: Compilation, Elaboration and Simulation.

![WhatsApp Image 2025-10-30 at 21 08 15_0eee078b](https://github.com/user-attachments/assets/4302862e-772f-4eb6-b295-ee362142825e)


#### Fig 3: Nclaunch Window

#### Step 1: Compilation:
– Process to check the correct Verilog language syntax and usage

Inputs: Supplied are Verilog design and test bench codes

Outputs: Compiled database created in mapped library if successful, generates report else error reported in log file

#####  Steps for compilation:
	Create work/library directory (most of the latest simulation tools creates automatically)
 
	Map the work to library created (most of the latest simulation tools creates automatically)
 
 Run the compile command with compile options
 
i.e Cadence IES command for compile: ncverilog +access+rwc -compile filename.v

Left side select the file and in Tools: launch verilog compiler with current selection will get enable. Click it to compile the code

Worklib is the directory where all the compiled codes are stored while Snapshot will have output of elaboration which in turn goes for simulation

![WhatsApp Image 2025-10-30 at 21 08 14_f8c21210](https://github.com/user-attachments/assets/34b4cd79-19e8-456e-9b9b-e132532be360)


#### Fig 4: Compiled database in WorkLib
After compilation, it will come under worklib. You can see on the right side window

select the test bench and compile it. It will come under Worklib. Under Worklib, you can see the module and test bench.

The cds.lib file is an ASCII text file. It defines which libraries are accessible and where they are located. It contains statements that map logical library names to their physical directory paths. For this Design, you will define a library called “worklib”

#### Step 2: Elaboration:
To check the port connections in a hierarchical design

Inputs: Top-level design/test bench Verilog codes

Outputs: Elaborate database updated in the mapped library if successful, generates a report, else error reported in the log file

#####  Steps for elaboration

– Run the elaboration command with elaborate options

1.It builds the module hierarchy

2. Binds modules to module instances
   
3.Computes parameter values

4. Checks for hierarchical name conflicts
   
5.It also establishes net connectivity and prepares all of this for simulation

After elaboration, the file will come under snapshot. Select the test bench and simulate it.

![WhatsApp Image 2025-10-30 at 21 08 09_11721f2d](https://github.com/user-attachments/assets/198bf59c-d56c-495c-9b1c-7b3c36fd75ce)



#### Fig 5: Elaboration Launch Option

#### Step 3: Simulation:
– Simulate with the given test vectors over a period of time to observe the output behaviour.

Inputs: Compiled and Elaborated top-level module name

Outputs: Simulation log file, waveforms for debugging

Simulations allow dumping design and test bench signals into a waveform

Steps for simulation – Run the simulation command with simulator options

![WhatsApp Image 2025-10-30 at 21 08 19_2e0ed74d](https://github.com/user-attachments/assets/310fa543-7799-41d3-af8e-c0753040692d)


#### Fig 6: Design Browser window for simulation

#### ALU CASE:
![WhatsApp Image 2025-10-30 at 21 08 20_851c680c](https://github.com/user-attachments/assets/8832687c-b86c-40f5-842e-87b61d07097f)


#### ALU IFELSE:
![WhatsApp Image 2025-10-30 at 21 08 17_1f01d937](https://github.com/user-attachments/assets/1786d1c7-ca86-4010-9f7a-f599c93d42f7)



#### Fig 7: Simulation Waveform Window

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

##### Performing Synthesis

##### Synthesize Design

Run the synthesis Process one time for each code and make sure the output File names are changed accordingly

The Liberty files are present in the library path,

• The Available technology nodes are 180nm,90nm and 45nm.

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist. Or use source run.tcl command in the terminal window to view the netlist, and a log file will be created in the working folder.

#### ALU CASE:
![WhatsApp Image 2025-10-30 at 21 08 18_c132f5d5](https://github.com/user-attachments/assets/7b494881-dd22-4dd0-aae5-e65006df705f)

#### ALU IFELSEIF:
![WhatsApp Image 2025-10-30 at 21 08 11_0deb0d42](https://github.com/user-attachments/assets/3c0f774a-41ba-4b38-93f9-9a52d091c2e8)


#### Fig 8: Synthesis RTL Schematic using case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (52)" src="https://github.com/user-attachments/assets/bc566c1b-272d-44ee-9568-9763ed980f80" />



#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (55)" src="https://github.com/user-attachments/assets/8b98067b-8fc3-4a90-83e1-dafe5e0c0f00" />


#### Fig 9: Area report of case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (49)" src="https://github.com/user-attachments/assets/2dcef559-9734-4d42-9897-92fc71ae8307" />


#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (56)" src="https://github.com/user-attachments/assets/78ceceb1-f556-4c87-afe5-1423f47f9341" />



#### Fig 10: Power Report of case and ifelseif construct

#### ALU CASE:
<img width="1920" height="1080" alt="Screenshot (54)" src="https://github.com/user-attachments/assets/756eaa41-b5a6-4b42-b4a2-91542751b71a" />


#### ALU IFELSEIF:
<img width="1920" height="1080" alt="Screenshot (57)" src="https://github.com/user-attachments/assets/76e50b44-8310-46a5-8553-a3fe9735a767" />


#### Fig 11: Timing Report of case and ifelseif construct



<img width="767" height="379" alt="image" src="https://github.com/user-attachments/assets/6ed19ba7-e03e-4c1b-aea5-9b4858a5cb3e" />

#### Fig 12: Tabulate Area,Power and Timing Report Comparision of ALU using case and ifelseif construct

## Result
The 32-bit ALU implemented using behavioural case statements and if–elseif constructs was successfully verified under Incisive (ncvlog/ncsim) for all tested vectors.A comparative analysis revealed that the case-statement-based ALU and the if–elseif-based ALU exhibited identical area and power consumption have no differnce Both implementations were functionally correct and synthesizable Both designs, however, produced identical functional outputs.
