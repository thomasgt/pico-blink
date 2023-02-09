# README

## Setup

### Linux

#### Visual Studio Code

Example `launch.json` file:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Pico Debug",
            "cwd": "${workspaceRoot}",
            "executable": "${command:cmake.launchTargetPath}",
            "request": "launch",
            "type": "cortex-debug",
            "servertype": "openocd",
            "gdbPath" : "gdb-multiarch",
            "objdumpPath": "arm-none-eabi-objdump",
            "device": "RP2040",
            "configFiles": [
                "interface/cmsis-dap.cfg",
                "target/rp2040.cfg"
            ],
            "openOCDLaunchCommands": ["adapter speed 5000"],
            "svdFile": "${env:PICO_SDK_PATH}/src/rp2040/hardware_regs/rp2040.svd",
            "runToMain": true,
            // Work around for stopping at main on restart
            "postRestartCommands": [
                "break main",
                "continue"
            ],
            "searchDir": ["${env:HOME}/.local/share/openocd/scripts"],
            "showDevDebugOutput": "raw"
        }
    ]
}
```
