## Area calculation using Yosys





harshamf@VSPANZER:~/yosys\_codes/project$ **yosys**



&nbsp;/----------------------------------------------------------------------------\\

&nbsp;|  yosys -- Yosys Open SYnthesis Suite                                       |

&nbsp;|  Copyright (C) 2012 - 2025  Claire Xenia Wolf <claire@yosyshq.com>         |

&nbsp;|  Distributed under an ISC-like license, type "license" to see terms        |

&nbsp;\\----------------------------------------------------------------------------/

&nbsp;Yosys 0.58+98 (git sha1 3d80e1663, g++ 13.3.0-6ubuntu2~24.04 -fPIC -O3)



yosys> **read\_liberty -lib NangateOpenCellLibrary\_typical.lib**



1\. Executing Liberty frontend: NangateOpenCellLibrary\_typical.lib

Imported 134 cell types from liberty file.



yosys> **read\_verilog synthapbslave.v**



2\. Executing Verilog-2005 frontend: synthapbslave.v

Parsing Verilog input from `synthapbslave.v' to AST representation.

verilog frontend filename synthapbslave.v

Generating RTLIL representation for module `\\top'.

Successfully finished Verilog frontend.



yosys> **hierarchy -top top**



3\. Executing HIERARCHY pass (managing design hierarchy).



3.1. Analyzing design hierarchy..

Top module:  \\top



3.2. Analyzing design hierarchy..

Top module:  \\top

Removed 0 unused modules.



yosys> **stat -liberty NangateOpenCellLibrary\_typical.lib**



4\. Printing statistics.



=== top ===



&nbsp;       +----------Local Count, excluding submodules.

&nbsp;       |        +-Local Area, excluding submodules.

&nbsp;       |        |

&nbsp;     476        - wires

&nbsp;     476        - wire bits

&nbsp;     476        - public wires

&nbsp;     476        - public wire bits

&nbsp;      55        - ports

&nbsp;      55        - port bits

&nbsp;     429  265.734 cells

&nbsp;     139        -   \\$\_DLATCH\_N\_

&nbsp;       3    3.192   AND2\_X1

&nbsp;       1    1.596   AND4\_X1

&nbsp;       8    8.512   AOI21\_X1

&nbsp;       2    10.64   DFFR\_X1

&nbsp;     125     66.5   INV\_X1

&nbsp;      23   18.354   NAND2\_X1

&nbsp;      20    21.28   NAND3\_X1

&nbsp;       8    10.64   NAND4\_X1

&nbsp;       6    4.788   NOR2\_X1

&nbsp;      28    37.24   NOR4\_X1

&nbsp;      17   18.088   OAI21\_X1

&nbsp;      48    63.84   OAI22\_X1

&nbsp;       1    1.064   OR2\_X1



&nbsp;  Area for cell type \\$\_DLATCH\_N\_ is unknown!



&nbsp;  **Chip area for module '\\top': 265.734000**

&nbsp;    of which used for sequential elements: 10.640000 (4.00%)





yosys>







**Context :**

 After Running abouve commands we got the area of the generated netlist based on the standard cell areas that are specified in the library file . we got , ***AREA OF APBSLAVE IP : 265.73 square micrometers.***











