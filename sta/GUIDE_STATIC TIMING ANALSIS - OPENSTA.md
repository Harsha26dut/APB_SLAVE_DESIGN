## STATIC TIMING ANALSIS - OPENSTA



harshamf@VSPANZER:~/yosys\_codes/project$ **cd ~**

harshamf@VSPANZER:~$ **cd OpenSTA**

harshamf@VSPANZER:~/OpenSTA$ **cd exp**

harshamf@VSPANZER:~/OpenSTA/exp$ **cp ~/yosys\_codes/project/synthapbslave.v ./top.v**

harshamf@VSPANZER:~/OpenSTA/exp$ **gedit top.v**

harshamf@VSPANZER:~/OpenSTA/exp$ **gedit top.sdc**

harshamf@VSPANZER:~/OpenSTA/exp$ **sta**

OpenSTA 2.7.0 585ff0c98b Copyright (c) 2025, Parallax Software, Inc.

License GPLv3: GNU GPL version 3 <http://gnu.org/licenses/gpl.html>



This is free software, and you are free to change and redistribute it

under certain conditions; type `show\_copying' for details.

This program comes with ABSOLUTELY NO WARRANTY; for details type `show\_warranty'.

% **source test.tcl**

.

.

.

.

.



### MAX TIMING ANALSIS- SETUP CHECK



**% report\_checks -path\_delay max -format full**

Startpoint: presetn (input port clocked by pclk)

Endpoint: \_716\_ (recovery check against rising-edge clock pclk)

Path Group: asynchronous

Path Type: max



&nbsp; Delay    Time   Description

---------------------------------------------------------

&nbsp;  0.00    0.00   clock pclk (rise edge)

&nbsp;  0.00    0.00   clock network delay (ideal)

&nbsp;  2.00    2.00 ^ input external delay

&nbsp;  0.00    2.00 ^ presetn (in)

&nbsp;  0.00    2.00 ^ \_716\_/RN (DFFR\_X1)

&nbsp;          2.00   data arrival time



&nbsp; 20.00   20.00   clock pclk (rise edge)

&nbsp;  0.00   20.00   clock network delay (ideal)

&nbsp;  0.00   20.00   clock reconvergence pessimism

&nbsp;         20.00 ^ \_716\_/CK (DFFR\_X1)

&nbsp;  0.05   20.05   library recovery time

&nbsp;         20.05   data required time

---------------------------------------------------------

&nbsp;         20.05   data required time

&nbsp;         -2.00   data arrival time

---------------------------------------------------------

&nbsp;         18.05   slack (MET)





Startpoint: penable (input port clocked by pclk)

Endpoint: pslverr (output port clocked by pclk)

Path Group: pclk

Path Type: max



&nbsp; Delay    Time   Description

---------------------------------------------------------

&nbsp;  0.00    0.00   clock pclk (rise edge)

&nbsp;  0.00    0.00   clock network delay (ideal)

&nbsp;  2.00    2.00 ^ input external delay

&nbsp;  0.00    2.00 ^ penable (in)

&nbsp;  0.01    2.01 v \_410\_/ZN (NAND2\_X1)

&nbsp;  0.02    2.03 ^ \_469\_/ZN (NOR2\_X1)

&nbsp;  0.00    2.03 ^ pslverr (out)

&nbsp;          2.03   data arrival time



&nbsp; 20.00   20.00   clock pclk (rise edge)

&nbsp;  0.00   20.00   clock network delay (ideal)

&nbsp;  0.00   20.00   clock reconvergence pessimism

&nbsp; -2.00   18.00   output external delay

&nbsp;         18.00   data required time

---------------------------------------------------------

&nbsp;         18.00   data required time

&nbsp;         -2.03   data arrival time

---------------------------------------------------------

&nbsp;         15.97   slack (MET)





### MINIMUM TIMING ANALSIS- HOLD CHECK





**% report\_checks -path\_delay min -format full**

Startpoint: presetn (input port clocked by pclk)

Endpoint: \_716\_ (removal check against rising-edge clock pclk)

Path Group: asynchronous

Path Type: min



&nbsp; Delay    Time   Description

---------------------------------------------------------

&nbsp;  0.00    0.00   clock pclk (rise edge)

&nbsp;  0.00    0.00   clock network delay (ideal)

&nbsp;  2.00    2.00 ^ input external delay

&nbsp;  0.00    2.00 ^ presetn (in)

&nbsp;  0.00    2.00 ^ \_716\_/RN (DFFR\_X1)

&nbsp;          2.00   data arrival time



&nbsp;  0.00    0.00   clock pclk (rise edge)

&nbsp;  0.00    0.00   clock network delay (ideal)

&nbsp;  0.00    0.00   clock reconvergence pessimism

&nbsp;          0.00 ^ \_716\_/CK (DFFR\_X1)

&nbsp;  0.18    0.18   library removal time

&nbsp;          0.18   data required time

---------------------------------------------------------

&nbsp;          0.18   data required time

&nbsp;         -2.00   data arrival time

---------------------------------------------------------

&nbsp;          1.82   slack (MET)





Startpoint: psel (input port clocked by pclk)

Endpoint: pslverr (output port clocked by pclk)

Path Group: pclk

Path Type: min



&nbsp; Delay    Time   Description

---------------------------------------------------------

&nbsp;  0.00    0.00   clock pclk (rise edge)

&nbsp;  0.00    0.00   clock network delay (ideal)

&nbsp;  2.00    2.00 v input external delay

&nbsp;  0.00    2.00 v psel (in)

&nbsp;  0.02    2.02 ^ \_410\_/ZN (NAND2\_X1)

&nbsp;  0.01    2.02 v \_469\_/ZN (NOR2\_X1)

&nbsp;  0.00    2.02 v pslverr (out)

&nbsp;          2.02   data arrival time



&nbsp;  0.00    0.00   clock pclk (rise edge)

&nbsp;  0.00    0.00   clock network delay (ideal)

&nbsp;  0.00    0.00   clock reconvergence pessimism

&nbsp; -2.00   -2.00   output external delay

&nbsp;         -2.00   data required time

---------------------------------------------------------

&nbsp;         -2.00   data required time

&nbsp;         -2.02   data arrival time

---------------------------------------------------------

&nbsp;          4.02   slack (MET)





%



**CONTEXT:**

 Timing analysis is done using OpenSTA tool , the design met the both setup and hold check constraints of timing.



 ***1. The "asynchronous" Path Group***

This group contains paths ending on asynchronous pins (like presetn or clear).



Recovery Check (Max Path): This verifies that the asynchronous signal is de-asserted (released) early enough

&nbsp;before the next clock edge so the flip-flop can capture the next data correctly without becoming metastable.



Removal Check (Min Path): This ensures the asynchronous signal remains inactive for a minimum time after the 

clock edge, similar to a hold check for reset signals.



***2. The "pclk" Path Group***

This group contains your standard synchronous data paths associated with your clock pclk.



Setup Check (Max Path): It checks the longest path from inputs (like penable) to outputs to ensure data

&nbsp;arrives within the clock period.



Hold Check (Min Path): It checks the shortest path (like from psel) to ensure data doesn't change too quickly

&nbsp;and corrupt the current state.







