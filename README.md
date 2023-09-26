# VATPRC VFPC Plugin
 
The VATPRC VFPC (VATSIM People's republic of China division Virtual Flight Plan Checker) is a plugin for EuroScope for VATPRC controllers to check flight plans against relevant route and altitude restrictions. 
Originally developed by hpeter2 and DrFreas, it has been expanded on with modified functionality to better suit by Justin Wai and Jamie Kong in HKvACC. You can find the codebase of the original plugin [here](https://github.com/hpeter2/VFPC). The Sid file for VATPRC is created and maintained by Ran Chen, a controller in VATPRC. This plugin is planned to be developed continuously for different airport. Anyone else willing to contribute to this project can send a email to the email: [here](2642608411@qq.com) with your real name, VATSIM CID, and home division.

As such, the code will continue to remain open source and free to download for any controllers. However, other divisions or subdivisions looking to implement or modify a similar flight plan checker may find the original plugin's versatility more useful.' However, please be advised that the GPLv3 copyright should not, and cannot be changed.

This plugin is still in active development, and may still contain bugs in the logic and general instability. Controllers, and especially new tower trainees (S1), should not rely on this plugin for all flight plan validation.
While it will greatly aid delivery controllers, it **does not negate the need for delivery controllers to thoroughly check every flight plan before release.** It cannot provide a solution to more major route issues. Especially for airports with an SOP, plz still use the SOP pdf file as it tells some SID exit point are primarily for some rwy.

VATPRC VFPC (VATSIM 中华人民共和国分部虚拟飞行计划检查器)是一个专为VATPRC管制员制作的航路计划检查插件。它的功能只要为：检查航路/巡航高度是否正确。

本项目原本由hpeter2 和 DrFreas制作，后经HKvACC的Justin Wai 和 Jaime Kong调整后本插件的性能有了非常大程度的提升。这个插件的原始GitHub page请见于 [here](https://github.com/hpeter2/VFPC)。本插件的Sid.json文件是由VATPRC分部的管制员Ran Chen 制作并维护的。这个项目仍在开发中，若有人也想参与制作，请邮件联系他：2642608411@qq.com。在你的申请中，请包含：真名，VATSIM CID 和你的分部，

请注意，这个插件仍在开发中，因此现在仍可能在逻辑上和稳定性上有所浮动。新管制员，尤其是S1管制员，请不要完全依赖此插件用作航路检查。即使这个插件可以很大程度上提升管制员的工作效率，它 **仍然要求所有管制员在给出放行之前详尽地检查计划**。在部分情况下，它不能提供非常准确的航路识别，尤其是在有SOP的机场。请你在这些机场进行管制时候仍然注重SOP pdf的使用，因为它无法分辨一些程序的主用跑道。

## Features:
- Tag function 'Check FP Menu': provide the possibility of choosing Show FLAS and Show ALL Checks
- Button function 'Show FLAS': State the able altitude or flight level
- Button function 'Show ALL Checks': Give the rationale for stating the altitude or route is right or wrong
- Chat command '.vfpc reload': reload the Sid.json config
- Chat command '.vfpc check': checks currently selected AC and outputs result
- Restrictions customizable in Sid.json config
- Checks Even/Odd Flightlevel restriction
- Checks Minimum & Maximum Flightlevel restriction
- Check condition 'route must contain airway' available
- Check condition 'destination must be' available
- Check condition 'aircraft type must be' available (? - unknown, P - piston, T - turboprop/turboshaft, J - jet, E - electric)

- 'Check FP Menu'会给到 'Show FLAS'和 'Show ALL Checks'两个选项
- 'Show FLAS'会显示可用高度
- 'Show ALL Checks' 会显示判定理由
- 聊天框指令 '.vfpc reload' 重新加载Sid.json
- 聊天框指令 '.vfpc check' 会检查机型和当前机型在该计划下的可用性
- 可自制的Sid.json
- 检查Even/Odd高度
- 检查最低（或最高可用）高度
- 可以自定义限制航路
- 可以自定义对于特定机场的高度
- 限制机型

## How to use:
- Load up the plugin VFPC.dll
- Add Tag Item type "VATPRC VFPC/VFPC" & function "VATPRC VFPC/ Check FP Menu" to Departure List, it is recommended to set the header name be VFPC and the width be 5

- 加载 VFPC.dll
- 在dep list添加 “VATPRC VFPC/VFPC", 然后设置左键/右键功能为"VATPRC VFPC/ Check FP Menu"。建议设置header name = VFPC, 宽度为5

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

CHK means the plugin fails to identify the route and failed to find an alt restriction for it. This may happen due to: First, mismatched SID according to the primary and secondary SID according to the SOP, Second: The pilot filed a route that is unavailable. Third: There is a bug in my Sid.json. If this happens, plz create a issue ticket in github and I will respond to it ASAP. 

OK! means that the route and altitude are both correct

FLR means that the alt that the pilot filed is incorrect according to the SOP. Also, plz let me know ASAP when the plugin considered a correct altitude wrong via Github.

会出现三种indication：OK!(绿), CHK(就是要你自己手动检查了, 红色), and FLR (高度不可用, 黄色)

CHK表示该插件无法检查改路线。可能的出现原因为：1. 跑道分配不可用（不符合SOP等）， 2. 提交的计划不可用，3. 我程序bug了。若出现这种情况，GitHub上开issue，我看到就回

FLR 表示高度错误。若是插件出问题了，立刻GitHub上开issue

## Notes for ZSPD
This plugin now **only support ZSPD**. The VFPC for ZSPD is made specifically for SOP ZSPD V2.03 amended on 7/21/2023. The VFPC status will indicate CHK when there is mismatched SID according to the primary and secondary SID and when the pilot's route disobey the ZSPD SOP v2.03

这个插件如今**只支持上海浦东**。这个VFPC 是根据SOP ZSPD V2.03（2023年7月21日修改版）制作的。这个VFPC只会检查SOP定义的主用和辅用离场跑道定义的程序，其余程序都会显示为CHK。


## How to I know the correct altitude
Left/Right click the FLR or CHK, click the show FLAS: It will indicate the correct altitude in a chatbox called VFPC. 

Left/Right click will also provide another option called Show ALL Checks. This will show in what respect does the plugin thinks this flight plan is wrong (or right)

根据您定义的左键或右键功能, 点击FLR/CHK/OK，点击 Show FLAS: 然后在聊天框会跳出一个叫 VFPC的框，会显示可用高度

根据您定义的左键或右键功能, 点击FLR/CHK/OK，点击 Show ALL Checks: 然后在聊天框会跳出判定依据

## Debug
If you get an error on load, please install the [latest C++ redistributables](https://aka.ms/vs/17/release/vc_redist.x86.exe)
若无法加载插件，请下载[最新的C++可再发行程序包](https://aka.ms/vs/17/release/vc_redist.x86.exe)

### How to define configurations
Examples can be found in the given Sid.json file.
定义的例子可以在Sid.json看

