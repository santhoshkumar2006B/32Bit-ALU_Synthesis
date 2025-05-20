# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)
![Screenshot 2025-05-20 115504](https://github.com/user-attachments/assets/6b01b64c-3c33-4910-8b38-f951f4c38572)


◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

Design Code:
module ALU ( input [3:0] A, B, input [2:0] ALU_Sel, output reg [3:0] ALU_Out, output regCarryOut );
```
always @(*) begin
  case (ALU_Sel)
    3'b000: {CarryOut, ALU_Out} = A + B;
    3'b001: {CarryOut, ALU_Out} = A - B;
    3'b010: ALU_Out = A & B;
    3'b011: ALU_Out = A | B;
    3'b100: ALU_Out = A ^ B;
    3'b101: ALU_Out = ~A;
    3'b110: ALU_Out = A << 1;
    3'b111: ALU_Out = A >> 1;
    default: ALU_Out =4'b0000;
  endcase
end
endmodule
```

TestBench:
module ALU_tb; reg [3:0] A, B; reg [2:0] ALU_Sel; wire [3:0] ALU_Out; wire CarryOut;
```
ALU uut (
     .A(A),
     .B(B),
     .ALU_Sel(ALU_Sel),
     .ALU_Out(ALU_Out),
     .CarryOut(CarryOut)
);
initial begin
    A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b000; #10;
    A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b001; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b010; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b011; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b100; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b101; #10;
    A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b110; #10;
    A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b111; #10;
    $finish;
end

endmodule
```
### Step 2 : Performing Synthesis

The Liberty files are present in the library path,
![Screenshot 2025-05-20 143935](https://github.com/user-attachments/assets/0fe02371-e8de-48fd-a4d7-c91b924f7b35)


• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc
![Screenshot 2025-05-20 144123](https://github.com/user-attachments/assets/b0dfdf7e-a892-40d5-818c-b3993e406f93)


• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![Screenshot 2025-05-20 115816](https://github.com/user-attachments/assets/44d488de-ca6c-47da-9361-57079fb70f41)


• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :

![Screenshot 2025-05-20 115654](https://github.com/user-attachments/assets/552d69a2-f168-4cd3-a6c9-ccab0d5ffbf8)


#### Area report:

![Screenshot 2025-05-20 120405](https://github.com/user-attachments/assets/76ca13c7-292e-414d-a649-1c13df201a32)


#### Power Report:

![Screenshot 2025-05-20 120501](https://github.com/user-attachments/assets/6c00f1c2-3d38-47a0-bdaa-1e961791a752)


#### Result: 

![Screenshot 2025-05-20 120227](https://github.com/user-attachments/assets/e3ec4dd0-2297-45ff-b84a-ddcfe627e184)


The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
