EXP-4

date:

               SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: o simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023.1.

APPARATUS REQUIRED:

Vivado 2023.1

PROCEDURE:

STEP:1 Launch the Vivado 2023.2 software.

STEP:2 Click on “create project ” from the starting page of vivado.

STEP:3 Choose the design entry method:RTL(verilog/VHDL).

STEP:4 Crete design source and give name to it and click finish.

STEP:5 Write the verilog code and check the syntax.

STEP:6 Click “run simulation” in the navigator window and click “Run behavioral simulation”.

STEP:7 Verify the output in the simulation window.

LOGIC DIAGRAM:
SR FLIPFLOP:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/e8324ee5-ef34-4385-a2d4-09ce9406798e)

VERILOG CODE:
```
module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
```

OUTPUT WAVEFORM:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/691975d3-55f8-46af-9853-5b53f728a1fe)

JK FLIPFLOP:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/dfb7f5cc-7583-46c2-9e95-f21d201b21bf)

VERILOG CODE :
```
module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)�        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```

OUTPUT WAVEFORM:
![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/1ada21ee-bd56-41ef-9c6d-74497f7d1d56)

T FLIPFLOP:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/8716fdd4-37cc-4c50-9595-6267a384d851)

VERILOG CODE:
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```

OUTPUT WAVEFORM:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/ec35702d-668c-46a2-8ff7-8e2dc552aa41)

D FLIPFLOP:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/18c5857f-2fa4-47eb-9d73-9afcd679a29b)

VERILOG CODE:
```
module DFlipFlop (D, clk, reset, Q) ;
input D;
input clk;
input reset; 
output reg Q; 
always @ (posedge clk)
begin
    if(reset == 1'b1)
        Q <= 1'b0;
    else
        Q <= D;
end
endmodule
```

OUTPUT WAVEFORM:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/d67a4b95-bba3-444b-a7de-1f5b7b501e30)

RIPPLE CARRY COUNTER:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/5bed12e4-9b42-4f04-8058-61df6da1ecf4)

VERILOG CODE:
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```

OUTPUT WAVEFORM:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/7ba01d56-8569-4a69-8e29-ae60ca76792a)

MOD 10 COUNTER VERILOG CODE:
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```

OUTPUT WAVEFORM:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/c06b0268-503b-4a5f-a4ee-a89acc951c6c)

UP DOWN COUNTER VERILOG CODE:
```
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```

OUTPUT WAVEFORM:

![image](https://github.com/Tarunkola1/VLSI-LAB-EXP-4/assets/161431337/80f1c47e-0f5c-43b8-a80a-0718e788c5e8)

RESULT:
THUS THE SIMULATION AND IMPLEMENTATION OF LOGIC GATES IS DONE AND VERIFIED
