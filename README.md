In this project, we modified a previously created pipelined CPU and added functionality to it to handle data dependencies and more in Verilog.
1. We synthesized the project given the original testbench and observed the outputs, and all of the
observed values seemed to match the testbench comments and output. This waveform without
forwarding displayed all of its expected values.
2. To complete 1 ahead forwarding, we originally started by rerouting the wires in the CPU (top
level module) to a forwarding unit that we created to handle one ahead forwarding. We added a
mux as an input to the ALU, whose inputs were ID/EX_A, WriteBackData, and MemAluOut, this
output goes into the A input of the ALU, whos select line is also determined by our forwarding
unit.
3. To complete 2 ahead forwarding we create another mux as an input to our ALU whose inputs
were ID/EX_B, writeBackData, and MemAluOut, which went into the B input of the ALU, whos
select line was determined again by our forwarding unit.
4. In our arbitration logic, we used the logic described in the pre-lab slides, where it checks the
values of registers in the ID/EX, EX/MEM, and MEM/WB stage to see whether or not they are
equal. Given the value of these comparisons, we selected 1 ahead or 2 ahead.
5. To add a check for $0 write, we added a check at the beginning of our loop that checks if the
EXMEM_Rd or MEMWB_Rd is == 0, and in the case that it is, we set the respective bits = 0
depending on which register is = 0.
6. For no write, we checked if the control signals in the registers were = 0, and if they were then we
also set their forwarding respective bits to 0.
7. We ran the waveforms for the register bypass, and given the values we can infer that they worked
as intended.
