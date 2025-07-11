# D Latch
##  Truth Table
```
 current state       Present State       Next State
    0                    0                 0
    0                    1                 1
    1                    0                 0
    1                    1                 1
```
## Design Code
```
module dlatch(clk,reset,d,q);
  input clk,reset,d;
  output reg q;
  always @(clk,reset,d)
  begin
    if(clk)
      if(reset)
        q<=1'b0;
    else
     q<=d;
    else
     q<=q;
  end
endmodule
```

## Testbench
```
module dlatch1;
  reg clk,reset,d;
  wire q;
  dlatch dut(clk,reset,d,q);
  initial begin
    clk=1'b0;reset=1'b0;d=1'b0;
    #2 clk=1'b0;reset=1'b0;d=1'b1;
    #2 clk=1'b1;reset=1'b1;d=1'b0;
    #2 clk=1'b1;reset=1'b0;d=1'b1;
    #2 clk=1'b1;reset=1'b1;d=1'b0;
  end
  initial begin
    $monitor("simtime=%0t,clk=%b,reset=%b,d=%b,q=%b",$time,clk,reset,d,q);
  end
  initial begin
    $dumpfile("dump.vcd");
    $dumpvars(0,dlatch1);
  end
endmodule
```
