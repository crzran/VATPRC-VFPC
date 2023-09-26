# VFPC Plugin
 
The VATPRC (VATSIM People's republic of China division Virtual Flight Plan Checker) is a plugin for EuroScope for VATPRC controllers to check flight plans against relevant route and altitude restrictions. 
Originally developed by hpeter2 and DrFreas, it has been expanded on with modified functionality to better suit by ACCHKG5 Justin Wai and Jamie Kong in HKvACC. You can find the codebase of the original plugin [here](https://github.com/hpeter2/VFPC). The Sid file for VATPRC is created and maintained by Ran Chen, a controller in VATPRC. This plugin is planned to be developed continuously for different airport.
As such, the code will continue to remain open source and free to download for any controllers. However, other divisions or subdivisions looking to implement or modify a similar flight plan checker may find the original plugin's versatility more useful.'

This plugin is still in active development, and may still contain bugs in the logic and general instability. Controllers, and especially new trainees, should not rely on this plugin for all flight plan validation.
While it will greatly aid delivery controllers, it **does not negate the need for delivery controllers to thoroughly check every flight plan before release.** It cannot provide a solution to more major route issues. Especially for airports with an SOP, plz still use the SOP pdf file as it tells some SID exit point are primarily for some rwy.

## Features:
- Tag item VFPC: Shows check-result as green 'OK!' or red 'FPL!' ('SID' = No valid SID found, 'ENG' = Failed Engine type restriction, 'E/O' = Failed even/odd Flightlevel, 'MIN' = Failed minimum Flight Level, 'MAX' = Failed maximum Flightlevel)
- Tag function 'Check FP': Explains the check-result in chat output
- Chat command '.vfpc reload': reload the Sid.json config
- Chat command '.vfpc check': checks currently selected AC and outputs result
- Restrictions customizable in Sid.json config
- Checks Even/Odd Flightlevel restriction
- Checks Minimum & Maximum Flightlevel restriction
- Check condition 'route must contain airway' available
- Check condition 'destination must be' available
- Check condition 'aircraft type must be' available (? - unknown, P - piston, T - turboprop/turboshaft, J - jet, E - electric)

## How to use:
- Load up the plugin
- Add Tag Item type & function to Departure List
- Extend the 'Sid.json' config file
![Departure List2](https://i.imgur.com/kQrtVfN.png)


### How to define configurations
The 'Sid.json'-File is using the JSON file format. Each airport is an object containing the "icao" and a sub-object "sids", which contains all definitions & restrictions. Inside this sub-object are all available SIDs defined by the first route waypoint (i.e. "AMLUH" for AMLUH1B, AMLUH9C, AMLUH9D & AMLUH9G).
Each SID can contain multiple objects with defined options based on restrictions. The plugin will stop at the first matching one from top-to-bottom, so the most restrictive objects should always be on top.

Available restrictions:
- "destinations" - Array of strings. The object only applies to FPL with one of the given destination ICAOs. Partials are possible, ex. "ED"
- "engine" - Either string or array of strings. The object only applies to AC with one of the given Engine Types. Options are "P" (piston), "T" (turboprop/turboshaft), "J" (jet) and "E" (electric), as defined by Euroscope
3 years ago

update the documentation
- "navigation" - A string which contains the equipment codes which defines all allowed capabilities for the SID
3 years ago

Update README.md
- "airways" - Array of strings. The object only applies to FPL if route contains any of the given airways

Available options:
- "direction" - String. The FPL must have this E/O option as final flightlevel. Available: "EVEN/ODD/ANY)
- "min_fl" - Integer. The FPL must have this flightlevel as minimum
- "max_fl" - Integer. The FPL must have this flightlevel as maximum

Examples can be found in the given Sid.json file.

## What will be seen
Three types of indications can be seen: OK!(in green), CHK(means check, in red), and FLR (means flight level wrong, in yellow)

CHK means the plugin fails to identify the route and failed to find an alt restriction for it. This may happen due to: First, mismatched SID according to the primary and secondary SID according to the SOP, Second: The pilot filed a route that disobey the ZSPD SOP v2. Third: There is a bug in my Sid.json. If this happens, plz create a issue ticket in github and I will respond to it ASAP. 

OK! means that the route and altitude are both correct

FLR means that the alt that the pilot filed is incorrect according to the SOP

## Notes for ZSPD
This plugin now **only support ZSPD**. Please note: this 


## How to I know the correct al·titude
Right click the FLR or CHK, click the show FLAS: It will indicate the correct altitude in a chatbox called VFPC. 

Right click will also provide another option called Show ALL Checks. This will show in what respect does the plugin thinks this flight plan is wrong (or right)

If you get an error on load, please install the [latest C++ redistributables](https://aka.ms/vs/17/release/vc_redist.x86.exe)

### How to define configurations
Examples can be found in the given Sid.json file.
