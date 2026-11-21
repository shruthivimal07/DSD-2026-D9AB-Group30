# Digital System Design – Group Project

> Complete every mandatory section. Do not delete headings. Replace bracketed prompts. If a section is not applicable, explain why.

## 1. Team Details
| Role | Student name | Roll number | GitHub username |
|---|---|---|---|
| Group leader | [Shruthi Vimalnath Nair] | [39] | [shruthivimal07] |
| Member 2 | [Krishna Pandey] | [45] | [KrishnaP45] |
| Member 3 | [Aryan Jadhav] | [18] | [aryannjadhavv15-rgb] |
| Member 4 | [Prarthana Gehani] | [15] | [prarthanagehani]|

**Class:** [D9A/D9B]  
**Group ID:** [D9A/B_Group30]  
**Repository URL:** [https://github.com/shruthivimal07/DSD-2026-D9AB-Group30.git]  
**Final Pull Request URL:** [URL]

## 2. Assigned Problem Statement
- **Number/title:** [ Group 30 - Gaming XP Level Decoder ]
- **Problem summary:** Given is a game xp level decoder with 4 bit input and a range decoder which decides which level the input belongs on. There are 3 level states- Beginner, Intermediate and Expert, which has a colour code. 
- **Objective:** Our objective in this PS is to convert the given FSM to a Mealy style machine, based on the current state and input.
- **Inputs and outputs:** Inputs: 4 bit Xp as our level ranges from 0-15. Output: states beginner, intermediate and expert, which are coloured leds of green, yellow and green respectively.
- **Constraints and assumptions:** As the our Machine is a Moore machine, needed to be converted into a Mealy Machine, We will use the inputs of the FSM dirctly to the output. Here, the input of the FSM is "start" and "ack". By these two inputs, we will feed to the register and the same inputs to the output, i.e. the LED.

## 3. Problem Analysis and Proposed Solution
Our problem Statement consisted of a gaming Level decoder, where at each level a coloured LED(green, yellow or red) lit for each level. It consisted of a 4 bit input switch, which passes through a 4-bit input register. This is, then, an input for the comparator. The comparator compares the levels  and then it lights the LED, dependng on what level  it is.

Our objective in this Problem is redesign the Gaming XP Level Decoder (4-bit XP, 0–15) as a Mealy FSM. The level output (BEGINNER / INTERMEDIATE / EXPERT) must be generated immediately from the current state and the current input XP[3:0], not only after the next clock edge. 


The solution we came up  with is to connect acknowledgment and start into the direct output  of the FSM. A mealy machine's key  feature is that  its output is always dependent on the input of the FSM. In this problem statement, our nputs are start, Acknowledgement, Beginner, Intermediate and Expert. Connecting these inputs together into the output would be the feasible solutionn for the problem.

## 4. Architecture


![Block diagram](Group_Submissions/D9A_Group30/07_Final_Report/BLOCK DIAGRAM.png)

## 5. FSM Design
Here is a short, simple explanation of each part:

1. **The Machine (Mealy FSM):** It has only two states (**IDLE** with `Q = 0` and **ACTIVE** with `Q = 1`) using one flip-flop. While *IDLE**, all LEDs stay OFF. While **ACTIVE**, the LEDs (`Beginner`, `Intermediate`, `Expert`) turn on immediately based on the 4-bit XP input (`0–3`, `4–10`, or `11–15`).


2. **The State Diagram:** Shows the two state circles (**IDLE** and **ACTIVE**) and the arrows between them. `start = 1` moves to ACTIVE`ack = 1` (without `start`) returns to IDLE, and `rst = 1` resets back to IDLE.


3. **The State Output Table:** Summarizes what happens in each state. When state `Q = 0` (**IDLE**), all LEDs are OFF for any input; when `Q=1` (**ACTIVE**), one LED turns ON depending on the XP range (`0–3` = Green, `4–10` = Yellow, `11–15` = Red).

**Diagram:** [Group_Submissions/D9A_Group30/07_Final_Report/STATE DIAGRAM.png] 
**State table:** [Group_Submissions/D9A_Group30/07_Final_Report/STATE TABLE.png]

## 6. Logisim Implementation
- Logisim version: [21.0.4]
- Circuit file: [Group_Submissions/D9A_Group30/02_FSM_Logisim/Xp_gameLvl_logisim.circ]
- Test cases and expected/observed behaviour: 
The FSM has four states: IDLE (00), BEGINNER (01), INTERMEDIATE (10) and EXPERT (11).
In IDLE, when START = 1, the output is generated right away from the current state and the XP value. The next state is set to the matching level state.
In a level state, the LED stays on until ACK = 1, after which the FSM goes back to IDLE.
RESET forces the FSM to IDLE and turns all LEDs off.
The next-state and output logic are combinational, and only the state register is clocked.
Because the output depends on the input as well as the state, the level shows up without the extra clock delay of the Moore version. This is the main difference between the two.

- Issues and corrections: [Details]
- Screenshot/evidence: [Path/link]

## 7. Verilog HDL Implementation
- Tool/version: [Xilinx Vivado, Vesion 2018.3]
- Top module and submodules: [xplvel.v, xpgaming_tb.v, xpmealy.xdc]
- Architecture/coding decisions: The type of modelling structure used in this code is Behavioural Modelling. 
- Synthesizability considerations: All code synthezied without any error and implemented sucessfully.
- RTL: `03_Verilog_Implementation/RTL/`
- Testbench: `03_Verilog_Implementation/Testbench/`

## 8. Verification and Simulation Results
| Test ID | Inputs/conditions | Expected output | Observed output | Pass/Fail |
|---|---|---|---|---|
| T01 | [ 0000 ] | [ Green light = on(1)] | [ Green light = 1 ] | [PASS] |
| T02 | [ 0101 ] | [ Yellow light = on(1) ] | [ Yellow Light = 1 ] | [PASS] |
| T03 | [ 1100 ] | [ Red light = on(1) ] | [ Red light = 1 ] | [PASS] |

Tool/version: [Xilinx Vivado 2018.3]  
Number passed/failed: [Pass]  
Waveform/log path: [Group_Submissions/D9A_Group30/05_Results/Waveform.png]

## 9. FPGA Hardware Implementation
- FPGA board/device: [Spartan 7]
- Tool/version: [Xilinx Vivado 2018.3]
- Clock/constraints: [Group_Submissions/D9A_Group30/04_FPGA_Hardware/xpmealy.xdc]
- Synthesis/implementation summary: All synthesis and implementation were done succesfully.
- Programming and hardware test result: [Pass]
- Evidence path: `04_FPGA_Hardware/`

Explain differences between simulation and hardware results, if any.

## 10. Challenges, Debugging and Improvements
| Issue | Root cause | Correction | Outcome |
|---|---|---|---|
| [ ] | [ ] | [ ] | [ ] |

Future improvements: [Details]

## 11. Task Allocation and Individual Contribution
| Student | Assigned responsibility | Actual contribution/evidence |
|---|---|---|
| Group leader | [Shruthi Vimalnath Nair] | [Github uploading and Logism] |
| Member 2 | [Prarthna Gehani ] | [ Logism and presentation] |
| Member 3 | [Krishna Pandey ] | [Verilog coding and Report writing] |
| Member 4 | [Aryan Jadhav ] | [Verilog coding and Report writing] |

Every student must be ready to explain the complete design.

## 12. Progress Log
Maintain time-wise updates in `STATUS.md`.

## 13. Final Results and Conclusion
We were able to create and convert a Moore Machine to a Mealy Machine. The topic, Gaming XP level decoder was succesfully implemented onto the Vivado 2018.3 software and was synthesised along with a testbench. Similarly, it was also impleneted onto the FPGA Spartan7 board, along with contraint file.

## 14. Team Reflection
We, as a team, learned the basics of the Finite State Machine(FSM) and conversion of the machines. We learnt about Moore, and Mealy in detail. Along with theory, we were able to learn Verilog and Logism basics, write constraint file and also how to implement on FPGA board. Other than the technical aspects, we learnt to collaborate together and work as a team.

## 15. Final Submission Checklist
- [DONE] Team details and problem analysis complete.
- [DONE] Architecture/block diagram included.
- [DONE] FSM diagram/table or justified alternative included.
- [DONE] Logisim source and simulation evidence uploaded.
- [DONE] Verilog RTL and testbench uploaded.
- [DONE] Simulation results and test cases documented.
- [DONE] FPGA implementation and hardware evidence uploaded.
- [DONE] Results, challenges and conclusion documented.
- [DONE] Presentation and final report uploaded.
- [DONE] STATUS.md is up to date.
- [DONE] Final Pull Request created and URL recorded.
