# Full Adder using Half Adder
## DESIGN
#### Half Adder
```
module half_adder(input a,b,
	          output sum,carry);
				 
   //Understand the Data-flow abstraction
   assign sum   = a ^ b;
   assign carry = a & b;

endmodule
	
```
#### Full Adder
```
module full_adder(a_in,
                  b_in,
		  c_in,
		  sum_out,
		  carry_out);

   //Step1 : Write down the directions for the ports	      
input a_in, b_in, c_in;
output sum_out, carry_out;

   //Step2 : Declare the internal wires    
wire w1,w2,w3;

   //Step3 : Instantiate the Half-Adders using name-based port mapping			 
half_adder HA1(.a(a_in),.b(b_in),.sum(w1),.carry(w2));
half_adder HA2(.a(w1),.b(c_in),.sum(sum_out),.carry(w3));

   //Step4 : Instantiate the OR gate

or OR1(carry_out,w2,w3);
endmodule
```
## TESTBENCH
```
module full_adder_tb();
		
   //Testbench global variables
   reg   a,b,cin;
   wire  sum,carry;

   //Variable for loop iteration 
   integer i;

   //Step1 : Instantiate the full adder with order based port mapping
full_adder DUT(.a_in(a),.b_in(b),.c_in(cin),.sum_out(sum),.carry_out(carry));

   //Process to initialize the variables at 0ns
   initial 
      begin
         a   = 1'b0;
	 b   = 1'b0;
  end
				
   //Process to generate stimulus using for loop
   initial
      begin 
	 for (i=0;i<8;i=i+1)
	    begin
	       {a,b,cin}=i;
	       #10;
	    end
      end
				
   //Process to monitor the changes in the variables
   initial 
      $monitor("Input a=%b, b=%b, c=%b, Output sum =%b, carry=%b",a,b,cin,sum,carry);
									
   //Process to terminate simulation after 100ns
   initial #100 $finish;
			  
endmodule
```
