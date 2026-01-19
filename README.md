


# Proofs 


forked the codespace as per instructions : https://github.com/varun-ms-s/vsd-riscv3 <br>

Proof of codespace usage below:
<img width="1561" height="915" alt="proof_of_codespace_usage" src="https://github.com/user-attachments/assets/5dcbc2aa-0e0a-4785-80d2-c25c7c328161" />
<br>


Screenshot of risc5 program i ran in workspace
<img width="1181" height="123" alt="risc5_out" src="https://github.com/user-attachments/assets/9d116755-96bc-424e-ac47-7d9114714f4b" />

<br>




Screenshot of fpga make run in workspace
<img width="1023" height="542" alt="fpga_output" src="https://github.com/user-attachments/assets/f022c647-db89-4113-bf0a-689ae40c60c4" />
<br>


LOCAL Linux setups proof

<img width="1838" height="1065" alt="fpgalab_firmware" src="https://github.com/user-attachments/assets/312e9989-1ac1-4138-a4d5-488437cebec5" />
<img width="1830" height="184" alt="toolchain_risc5" src="https://github.com/user-attachments/assets/88c4f748-aebd-42d1-bb23-8328590078f1" />



# Questions and Answers
<br>
1.Where is the RISC-V program located in the vsd-riscv2 repository?<br>
ans: Program is in samples folder with filename sum1ton.c <br>
<br>
2.How is the program compiled and loaded into memory<br>
ans:riscv64-unknown-elf-gcc compiler compiles the code as per risc5 instructions and creates binary file sum1ton.o. This binary file is run with spike risc5 simulator to see the output.<br>
<br>
3.How does the RISC-V core access memory and memory-mapped IO?<br>
ans:RISC-V uses a flat memory address space where each address points to a byte of memory. The processor accesses memory through Load/Store instructions.Risc5 treats each memory mapped IO as a register which has a memory address where we can store or load certain value usin risc5 native instructions.Foe example in The Git repo i see THe base address for output ports is 0x400000  (#define IO_BASE       0x400000) and there is function which returns physical address based in port number IO_IN(port) = *(volatile uint32_t*)(IO_BASE + port) (if port number is 4 the address for that port will 0x400004.Then we can write risc5 program with load ,store ,add or any memory accessing instruction with this address to do any operation on the data at this port <br>
<br>
4.Where would a new FPGA IP block logically integrate in this system?<br>
ans:New FPGA block will be outside RIsc5(Processor)  core in module SOC with certain section of memory space of Risc5 mapped to it.So that Risc5 can access or modify the the config values of FPGA which will control the functionality of IP.Risc5 will provide the firmware which direvts how the IP will behave.Also Fpga IP can be use to ofload cpu from some tasks like timers where RISC 5 cpu core can send start and fetch the timer output from TIMER IP which does the counting task.<br>



