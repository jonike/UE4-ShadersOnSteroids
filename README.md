*(Tested on 4.25.4. Works on Windows platform only.)*

Working with materials or loading a big batch of meshes with complex materials can add up to a lot of shaders to compile. If you want this process to be way faster, this code can automatically raise or lower the priority of all ShaderCompileWorkers that are instanced when there are shaders to compile.

If you have the source version of UE4, you can replace your ShaderCompiler.cpp at:

`...\Engine\Source\Runtime\Engine\Private\ShaderCompiler`

and then rebuild your engine.

Changes from the vanilla version of Epic's .cpp is the inclusion of HAL/ConsoleManager.h and Windows libraries that allow for tinkering with the priority of running processes. Exact changes at the commit's description.

The first time a ShadowCompileWorker is spawned per engine instance, a `wildmode` command variable is created. You can call this from your usual engine console. Accepted values are 0 for "Below normal" priority (default) or 1 for "High" priority.

![CmdExample](CmdExample.jpg)\
*"wildmode 0" and "wildmode 1" are the valid commands.*

Then, workers priority is set from the value returned from PriorityModifierFromCommand(), at spawn and periodically on runtime. The runtime check for priority happens between worker "jobs", so it might take a couple of seconds to update if you're currently compiling shaders.

-----------------------------------------------------

*If you have any other inquiries, feel free to contact me on Discord at __Ertie#1858__!*\
*Or at [Twitter](http://twitter.com/Ertie_exe)!!*