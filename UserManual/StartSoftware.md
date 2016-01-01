# Start Software

## Installing prerequisites
You should only need to install the prerequisites once.  

The Flexostat software depends on python 2.7.9 or later (3.x is untested and likely incompatible).  

1. Install the latest python 2.7.x from either your systems package repository or [python.org](http://python.org).  Windows users can and probably should install [pythonxy](http://python-xy.github.io/) (or any other python distribution that includes numpy) and skip the next step.
2. Install numpy following the directions at the [numpy website](http://www.numpy.org/)
  * On some platforms you may be able to install numpy with
    ```
    sudo pip install numpy
    ```
3. Install pyserial and pygments using pip
  * From the command line, run (Note: Linux and MacOS may need to preceed these commands with `sudo`):
    ```
    pip install pyserial
    pip install pygments
    ```

## Downloading Flexostat software
The latest flexostat software can be downloaded from the flexostat github repository or directly downloaded  [here](https://github.com/klavinslab/Flexostat-interface/archive/master.zip).

## Configuring the software

Below is an annotated version of a typcial `config.ini`

```
[controller]
;don't inclued the .py
controlfun: turbidostatController
kp: 3.0
ki: 0.05
; space seperated list of setpoints
setpoint: 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0
altsetpoint: 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0
odperiod: 4
maxdilution: 160.0
mindilution: 7.0
period: 60
baudRate: 19200
```
This section contains controller related parameters.
*  `;`: anything starting with `;` is a comment and not read by the software.
*  `controlfun`:  The name of the controller function in the `plugins/` directory.  Do not include the `.py`.
*  `kp`,`ki`: The proportional and integral control parameters.  You shouldn't need to change these.
*  `setpoint`: A space separated list of OD setpoints for chambers 1 through 8 respectively
*  `altsetpoint`: The secondary OD setpoints for square wave and sin wave controllers.  Ignored by other controllers.
*  `odperiod`: The period, in hours, for square wave and sin wave controllers.  Ignored by other controllers.
*  `maxdilution`, `mindilution`: The maximum and minimum dilution rates in the native pump units.  The minimum should be set high enough to prevent liquid loss due to evaporation.  The maximum should be roughly 1/10th the syringe volume or 160 for the servo syringe.
*  `period`: The dilution cycle period in seconds.
*  `baudRate`: The mainboard's baudrate.  This shouldn't ever change.

```
[log]
odlog: odlog.dat
fulllog: log.dat
errorlog: errors.log
blanklog: blank.dat
```
This section specifies where log files go.  Paths are relative to the program directory.  By default log files are appended to, so to start a new experiment delete or move the old .dat and .log files.  
*  `odlog`: This is the primary log file containing ODs and dilution rates.
*  `fulllog`: This log contains the raw data.  It is mostly for debug.
*  `errorlog`: This log contains any caught but nonfatal exceptions.  It is mostly for debug.
*  `blanklog`: This file contains the reference values for OD calculation.  If this file already exists it is used as the blank.  Otherwise a new blank is taken and saved to this file.

```
[ports]
controllerPort: COM1
; use NONE for cheapostat
pumpPort: NONE
network:3399
```

This section tells the software what ports are used by the Flexostat.  
*  `controllerPort`: The serial port that the mainboard is plugged into.
*  `pumpPort`: Use `NONE` for the servo pump.  For other pumps (eg NE-500) use the serial port that the pump is attached to.
*  `network`: Reserved for future use.

```
[pump]
;don't include the .py
roundingfix: false
pumpdriver: cheapopumpdriver
baudRate: 19200
syringeDiameter: 7.290
volumeUnits: UL
syringeRate: 1800
syringRateUnit: UM
```

This section contains pump parameters.  

*  `roundingfix`: Set to `true` to work around rounding errors in pump volume calculations.  Currently this only needs to be true for the NE-500 pump.
*  `pumpdriver`: The filename for the code that drives the pump.  `cheapopumpdriver` for the servo pump, `ne500pumpdriver` for the NE-500 pump.  
*  `baudRate`: The baud rate for external syringe pumps.  
*  `syringeDiameter`:  Syringe diameter setting.  Ignored by cheapopumpdriver.
*  `volumeUnits`:  NE-500 volume units.  Ignored by cheapopumpdriver.
*  `syringeRate`:  NE-500 pumping rate setting.  Ignored by cheapopumpdriver.
*  `syringeRateUnit`:  NE-500 pumping rate unit setting.  Ignored by cheapopumpdriver.
