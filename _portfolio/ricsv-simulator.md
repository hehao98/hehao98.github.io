---
title: "RISC-V Simulator"
excerpt: "A Simple RISC-V CPU Simulator with 5 Stage Pipeline, Branch Prediction and Cache Simulation"
collection: portfolio
---

It is a simple RISC-V Emulator suppprting user mode RV64I instruction set, from PKU Computer Architecture Labs, Spring 2019. I made my project open source in the hope that others can learn from my code about how to make a CPU Emulator and get a deeper understanding in computer architecture.

Here is an example of its execution.

```
hehaodeMacBook-Pro:build hehao$ ./Simulator ../riscv-elf/helloworld.riscv
Hello, World!
Program exit from an exit() system call
------------ STATISTICS -----------
Number of Instructions: 141
Number of Cycles: 188
Avg Cycles per Instrcution: 1.3333
Branch Perdiction Accuacy: 0.5833 (Strategy: Always Not Taken)
Number of Control Hazards: 23
Number of Data Hazards: 73
Number of Memory Hazards: 1
-----------------------------------
hehaodeMacBook-Pro:build hehao$ ./Simulator ../riscv-elf/test_arithmetic.riscv
30
-10
370350
411
49380
771
Program exit from an exit() system call
------------ STATISTICS -----------
Number of Instructions: 508
Number of Cycles: 703
Avg Cycles per Instrcution: 1.3839
Branch Perdiction Accuacy: 0.4268 (Strategy: Always Not Taken)
Number of Control Hazards: 91
Number of Data Hazards: 224
Number of Memory Hazards: 13
-----------------------------------
hehaodeMacBook-Pro:build hehao$ ./Simulator ../riscv-elf/test_syscall.riscv
This is string from print_s()
123456abc
Enter a number: 123456
The number is: 123456
Enter a character: g
The character is: g
Program exit from an exit() system call
------------ STATISTICS -----------
Number of Instructions: 350
Number of Cycles: 461
Avg Cycles per Instrcution: 1.3171
Branch Perdiction Accuacy: 0.5833 (Strategy: Always Not Taken)
Number of Control Hazards: 53
Number of Data Hazards: 178
Number of Memory Hazards: 5
-----------------------------------
hehaodeMacBook-Pro:build hehao$ ./Simulator ../riscv-elf/quicksort.riscv
Prev A: 5 3 5 6 7 1 3 5 6 1 
Sorted A: 1 1 3 3 5 5 5 6 6 7 
Prev B: 100 99 98 97 96 95 94 93 92 91 90 89 88 87 86 85 84 83 82 81 80 79 78 77 76 75 74 73 72 71 70 69 68 67 66 65 64 63 62 61 60 59 58 57 56 55 54 53 52 51 50 49 48 47 46 45 44 43 42 41 40 39 38 37 36 35 34 33 32 31 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 
Sorted B: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85 86 87 88 89 90 91 92 93 94 95 96 97 98 99 100 
Program exit from an exit() system call
------------ STATISTICS -----------
Number of Instructions: 103671
Number of Cycles: 141697
Avg Cycles per Instrcution: 1.3668
Branch Perdiction Accuacy: 0.4926 (Strategy: Always Not Taken)
Number of Control Hazards: 7314
Number of Data Hazards: 86448
Number of Memory Hazards: 23398
-----------------------------------
hehaodeMacBook-Pro:build hehao$ ./Simulator ../riscv-elf/matrixmulti.riscv
The content of A is: 
0 0 0 0 0 0 0 0 0 0 
1 1 1 1 1 1 1 1 1 1 
2 2 2 2 2 2 2 2 2 2 
3 3 3 3 3 3 3 3 3 3 
4 4 4 4 4 4 4 4 4 4 
5 5 5 5 5 5 5 5 5 5 
6 6 6 6 6 6 6 6 6 6 
7 7 7 7 7 7 7 7 7 7 
8 8 8 8 8 8 8 8 8 8 
9 9 9 9 9 9 9 9 9 9 
The content of B is: 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
0 1 2 3 4 5 6 7 8 9 
The content of C=A*B is: 
0 0 0 0 0 0 0 0 0 0 
0 10 20 30 40 50 60 70 80 90 
0 20 40 60 80 100 120 140 160 180 
0 30 60 90 120 150 180 210 240 270 
0 40 80 120 160 200 240 280 320 360 
0 50 100 150 200 250 300 350 400 450 
0 60 120 180 240 300 360 420 480 540 
0 70 140 210 280 350 420 490 560 630 
0 80 160 240 320 400 480 560 640 720 
0 90 180 270 360 450 540 630 720 810 
Program exit from an exit() system call
------------ STATISTICS -----------
Number of Instructions: 225441
Number of Cycles: 318532
Avg Cycles per Instrcution: 1.4129
Branch Perdiction Accuacy: 0.3765 (Strategy: Always Not Taken)
Number of Control Hazards: 40678
Number of Data Hazards: 110957
Number of Memory Hazards: 11735
-----------------------------------
hehaodeMacBook-Pro:build hehao$ ./Simulator ../riscv-elf/ackermann.riscv
Ackermann(0,0) = 1
Ackermann(0,1) = 2
Ackermann(0,2) = 3
Ackermann(0,3) = 4
Ackermann(0,4) = 5
Ackermann(1,0) = 2
Ackermann(1,1) = 3
Ackermann(1,2) = 4
Ackermann(1,3) = 5
Ackermann(1,4) = 6
Ackermann(2,0) = 3
Ackermann(2,1) = 5
Ackermann(2,2) = 7
Ackermann(2,3) = 9
Ackermann(2,4) = 11
Ackermann(3,0) = 5
Ackermann(3,1) = 13
Ackermann(3,2) = 29
Ackermann(3,3) = 61
Ackermann(3,4) = 125
Program exit from an exit() system call
------------ STATISTICS -----------
Number of Instructions: 430754
Number of Cycles: 574548
Avg Cycles per Instrcution: 1.3338
Branch Perdiction Accuacy: 0.5045 (Strategy: Always Not Taken)
Number of Control Hazards: 48010
Number of Data Hazards: 279916
Number of Memory Hazards: 47774
-----------------------------------
```