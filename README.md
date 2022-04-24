# arma-3-life-reporting

This is a script to centrally coordinate police or medic units for ArmA 3 RPG Life.

## Installation

A working installation of ArmA Life RPG Framework is required for a successful installation. Modifying the ArmA Life RPG Framework could cause errors – feel free to connect to our discord if you have a problem.

### Step 1

Download the newest release and extract the archive. Copy the folder "reporting" in your “cation” folder that can be found in the  root folder (subsequently called \<mission\>) of your mission.

### Step 2

Open \<mission\>/cation/cation_functions.cpp and insert

`#include "reporting\functions.cpp"`

and save the file.

### Step 3

Open \<mission\>/cation/cation_master.cpp and insert

`#include "reporting\config.cpp"`

and save the file.

### Step 4

Open \<mission\>/cation/cation_remoteExec.cpp and insert

`#include "reporting\remoteExec.cpp"`

and save the file.

### Step 5

Create two new buttons to your y-menu (\<mission\>/dialog/player_inv.hpp). Insert the following code to the control center button

`onButtonClick = "closeDialog 0; [] call cat_reporting_fnc_createDialogControlCenter;";`

and insert the next code to the unit’s radio button:

`onButtonClick = "closeDialog 0; [] call cat_reporting_fnc_createDialogUnit;";`

Afterwards save the file.

**Example:**

```
class FMSCenter: Life_RscButtonMenu {
    idc = 2017;
    text = "Control Center";    
    onButtonClick = "closeDialog 0; [] call cat_reporting_fnc_createDialogControlCenter;";    
    x = 0.1 + (6.25 / 19.8) + (1 / 250 / (safezoneW / safezoneH));    
    y = 0.805;    
    w = (6.25 / 40);    
    h = (1 / 25);
};
class FMS: Life_RscButtonMenu {    
    idc = 2019;    
    text = "Radio";    
    onButtonClick = "closeDialog 0; [] call cat_reporting_fnc_createDialogUnit;";    
    x = 0.1 + (6.25 / 40) + (1 / 250 / (safezoneW / safezoneH));    
    y = 0.805;    
    w = (6.25 / 40);    
    h = (1 / 25);
};
```

### Step 6

In your \<mission\>/core/pmenu/fn_p_openMenu.sqf add to case civilian

`ctrlShow[2019,false];ctrlShow[2017,false];`

and to case west

```
if ((call life_coplevel) >> (getNumber(missionConfigFile >> "Cation_Reporting" >> "controlCenterMinLevelWest"))) then {
    ctrlShow[2017,false];
};
```
and to case independent

```
if ((call life_mediclevel) >> (getNumber(missionConfigFile >> "Cation_Reporting" >> "controlCenterMinLevelIndependent"))) then {
    ctrlShow[2017,false];
};
```

and save the file.

**That’s it!**

You have installed the cationstudio reporting system successfully!

## Configuration

You can adjust settings in \<mission\>/cation/reporting/config.cpp.

In the settings it is important to set ArmA Life version to your used version.

Texts and translations can be edited in \<mission\>/cation/reporting/language.cpp.