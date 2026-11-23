**Problem Statement:**
Our problem Statement consisted of a gaming Level decoder, where at each level a coloured LED(green, yellow or red) lit for each level. It consisted of a 4 bit input switch, which passes through a 4-bit input register. This is, then, an input for the comparator. The comparator compares the levels  and then it lights the LED, dependng on what level  it is. 

Our goal is to redesign the Gaming XP Level Decoder (4-bit XP, 0–15) as a Mealy FSM. The level output (BEGINNER / INTERMEDIATE / EXPERT) must be generated immediately from the current state and the current input XP[3:0], not only after the next clock edge. Draw the Mealy state diagram, then implement and verify it in Logisim and Verilog.

XP 0–3 should show BEGINNER, 4–10 INTERMEDIATE and 11–15 EXPERT.
Outputs must depend on both the present state and the input XP[3:0].
START loads the XP value, ACK sends the FSM back to IDLE, and RESET is synchronous and active-high.

Inputs and Outputs:
CLK -> Input -> System clock
2. RESET -> Input -> Synchronous reset, active-high
3. XP[3:0] -> Input -> 4-bit XP value
4. START -> Input -> Starts decoding and samples XP
5. ACK -> Input -> Acknowledge, returns the FSM to IDLE
6. BEGINNER_LED -> Output -> High for XP 0–3
7. INTERMEDIATE_LED -> Output -> High for XP 4–10
8. EXPERT_LED -> Output -> High for XP 11–15

**Proposed Solution:**
The FSM has four states: IDLE (00), BEGINNER (01), INTERMEDIATE (10) and EXPERT (11).
A range decoder compares XP and finds which range it falls in: ≤3, 4 to 10, or ≥11.
In IDLE, when START = 1, the output is generated right away from the current state and the XP value. The next state is set to the matching level state.
In a level state, the LED stays on until ACK = 1, after which the FSM goes back to IDLE.
RESET forces the FSM to IDLE and turns all LEDs off.
The next-state and output logic are combinational, and only the state register is clocked.
Because the output depends on the input as well as the state, the level shows up without the extra clock delay of the Moore version. This is the main difference between the two.

1. State Diagram: Group_Submissions/D9A_Group30/07_Final_Report/STATE DIAGRAM.png
2. State Table: Group_Submissions/D9A_Group30/07_Final_Report/STATE TABLE.png

**Results:** 

1. Logisim: Group_Submissions/D9A_Group30/07_Final_Report/LOGISIM.png
2. Verilog: Group_Submissions/D9A_Group30/03_Verilog_Implementation/RTL/xplevel.v
3. Fpga Implemetation: Group_Submissions/D9A_Group30/04_FPGA_Hardware/FPGA WORKING.mp4

**Conclusion:**
We were able to create and convert a Moore Machine to a Mealy Machine. The topic, Gaming XP level decoder was succesfully implemented onto the Vivado 2018.3 software and was synthesised along with a testbench. Similarly, it was also impleneted onto the FPGA Spartan7 board, along with contraint file.