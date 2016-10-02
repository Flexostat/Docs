## Introduction
The Flexostat's main components have gone through several iterations, 
some of which break compatibility.  There are two primary reasons for 
new versions.  The first is improvements in accuracy, ease of assembly
or reliability.  The second reason is to work around components that
are no longer available.  

Below you will find a list of compatible components and in some cases
a compatability matrix.

## OD Board

#### OD Board and chamber
| chamber\OD board | older | v3.2 | v3.3 | v3.4 |
|------------------|-------|------|------|------|
| 1.0              | some  | yes  | yes  | no   |
| 2.0              | ?     | yes  | yes  | no   |
| 2.1              | ?     | yes  | yes  | no   |
| 2.2              | ?     | yes  | yes  | no   |
| 2.3              | ?     | yes  | yes  | yes  |

#### OD Board and steppers
any 12v 48 step per revolution stepper should work with v3.3 and v3.4.  Prior to v3.3 steppers were driven by a 5v full step signal assuming 48 steps/revolution.  Currently the ST-PM35-15-11C is recommended (available from sparkfun and around the internet).  Spending more money will probably get you a better motor, but make sure it has 48 steps/revolution.  
