# 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task

# Aim
To design and simulate a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment. 

# Apparatus Required
Vivado 2023.1
# Procedure
1. Launch Vivado 2023.1
Open Vivado and create a new project.
2. Design the Verilog Code
Write the Verilog code for the seven-segment display, defining the logic that maps a 4-bit binary input to the corresponding segments (a to g) of the display.
3. Create the Testbench
Write a testbench to simulate the seven-segment display behavior. The testbench should apply various 4-bit input values and monitor the corresponding output.
4. Create the Verilog Files
Create both the design module and the testbench in the Vivado project.
5. Run Simulation
Run the behavioral simulation to verify the output. 
6. Observe the Waveforms
Analyze the output waveforms in the simulation window, and verify that the correct segments light up for each digit.
7. Save and Document Results
Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# Verilog Code
# 4 bit Ripple Adder using Task
```verilog
module ripcar (input  [3:0] a,input  [3:0] b,input cin,output reg [3:0] sum,output reg cout
);
integer i;
reg c;
    task full_adder;
        input a, b, cin;
        output s, cout;
        begin
            s    = a ^ b ^ cin;
            cout = (a & b) | (b & cin) | (a & cin);
        end
    endtask
    always @(*) begin
    c = cin;
    for (i = 0; i < 4; i = i + 1) begin
        full_adder(a[i], b[i], c, sum[i], c);
    end
    cout = c;
    end
endmodule
```

# Test Bench
```verilog
module ripcar_tb;
    reg  [3:0] a, b;
    reg        cin;
    wire [3:0] sum;
    wire       cout;

    ripcar uut (a, b, cin, sum, cout);

    initial begin
        $monitor("Time=%0t | a=%b b=%b cin=%b | sum=%b cout=%b",
                  $time, a, b, cin, sum, cout);

        a=4'b0000; b=4'b0000; cin=0;
        #10 a=4'b0101; b=4'b0011; cin=0;
        #10 a=4'b1111; b=4'b0001; cin=0;
        #10 a=4'b1010; b=4'b0101; cin=1;
        #10 a=4'b1111; b=4'b1111; cin=1;
        #10 $finish;
    end
endmodule
```
# Output Waveform
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/04826c3a-d45d-4825-b74f-b87183f2db4e" />

# 4 bit Ripple counter using Function
```verilog
module ripple_counter_func (
    input clk, rst,
    output reg [3:0] Q
);
    function [3:0] count;
        input [3:0] x;
        begin
            count = x + 1;   
        end
    endfunction
    always @(posedge clk or posedge rst) begin
     if (rst)
           Q <= 4'b0000;     
       else
            Q <= count(Q);    
    end
endmodule

```
# Test Bench
```verilog

module ripple_counter_tb;
    reg clk, rst;
    wire [3:0] Q;
    ripple_counter_func uut (
        .clk(clk),
        .rst(rst),
        .Q(Q)
    );
    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end
    initial begin
        rst = 1;
        #12;
        rst = 0;
        #200;
        rst = 1;
        #10;
        rst = 0;
        #100;
        $finish;
    end
endmodule
```
# Output Waveform 

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/be6f8ba4-7887-479f-bd1f-92393d5752d6" />

# Conclusion
In this experiment, a 4-bit-Ripple-counter-using-Function-and-4-bit-Ripple-Adder-using-task was successfully designed and simulated using Verilog HDL.
