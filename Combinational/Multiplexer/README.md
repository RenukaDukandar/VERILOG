# 4:1 MUX using 2:1 MUX
## DESIGN
```
module mux4x1_2x1(I,S,Y);
  input[3:0]I;
  input[1:0]S;
  output Y;

  wire W1,W2;
 
    mux2x1 M1(I[0], I[1], S[0], W1);
    mux2x1 M2(I[2], I[3], S[0], W2);
    mux2x1 M3(W1, W2, S[1], Y);

endmodule
```
## TESTBENCH
```
module mux4x1_2x1_tb();

    reg [3:0] I;
    reg [1:0] S;
    wire Y;

    // Instantiate 4:1 MUX
    mux4x1_2x1 DUT(I, S, Y);

    // Task for stimulus
    task stimulus;
        input [3:0] i;
        input [1:0] s;
        begin
            I = i;
            S = s;
            #10;
        end
    endtask

    initial begin
           
        $monitor("values of I=%b, S=%b, Y=%b", I, S, Y);

        stimulus(4'b1010, 2'b00);
        stimulus(4'b0101, 2'b01);
        stimulus(4'b1011, 2'b10);
        stimulus(4'b1111, 2'b11);
        stimulus(4'b1001, 2'b00);
        stimulus(4'b0110, 2'b01);
        stimulus(4'b1100, 2'b10);
        stimulus(4'b0011, 2'b11);
        stimulus(4'b1011, 2'b01);
        stimulus(4'b0100, 2'b01);

        $finish;
    end

endmodule
```
