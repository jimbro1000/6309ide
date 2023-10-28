# 8 Bit IDE for 6309 SBC #

Inspired (and partially copied from) Breadbording Labs 
(https://www.youtube.com/@breadboardinglabs) which is,
in turn, taken from other existing 8 bit IDE projects.

This design is configured to work with my 6309 SBC 
project.

## Status ##

This is a work in progress and is not ready for production.
The two SEL lines are not wired and need some address selection
logic to fit the design to the available mapped memory

## Drivers ##

The IDE operation requires software drivers to simplify
operation. It also needs programming for the GAL

### GAL Definition ###

Input (1-9):  
A0, A4, A5, A6, A6, E, SEL0, RW, SEL1

Output (19-12):  
!UDW, !UDR, !LDW, !IOW, !IOR, !CS0, !CS1, !LDR

ACT = !A5 & !A6 & !A7 & !SEL0

CS0 = !A4 & ACT  
CS1 = A4 & ACT  
IOR = !A0 & ACT & RW  
IOW = A0 & ACT & !RW  
LDR = !A0 & ACT & RW  
LDW = !A0 & ACT & !RW  
UDR = A0 & ACT & RW  
UDW = A0 & ACT & !RW

(note: IOR and LDR are the same)