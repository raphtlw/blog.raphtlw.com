This post contains all the scripts/utilities/tools I use when setting up a brand new Windows installation. In chronological order.

Previously used a window manager, but since Windows has a built-in one (dwm.exe), and is so hooked deep into the system, I can't get rid of it, so I just decided to use it.

1. Remove all icons from the start menu
2. Remove all taskbar icons
3. Sign in to Windows
4. Hide all icons from the desktop
5. Install Arc, Brave, use Edge for Microsoft-related stuff, and school account.
6. Install and enable WSL2
7. Install Git for Windows
8. Install Discord and Vencord
9. Install AutoHotKey
10. Install PowerToys
11. Disable Game Capture, use OBS instead
12. Uninstall Snipping Tool, use ShareX instead
13. Setup OBS and configure settings, install [OBS audio monitor plugin](https://obsproject.com/forum/resources/audio-monitor.1186/)
14. Uninstall Media Player, use VLC instead
15. Use FanControl software to configure fan curves
16. Disable Indexing and use Everything instead

## Programs

Motherboard software
HWINFO
Inter fonts
OpenRGB
SerialRGB
Bitwarden
macOS cursors
Logitech G-HUB
Arc Browser
PowerToys
NVIDIA App
iCloud
Prism Launcher
SharpKeys
Twinkle Tray
OBS
UVR
Unigram
IconViewer
Everything
BCUninstaller
EverythingToolbar
Wintoys
FxSound
VLC Media Player
AutoHotkey
nircmd
ShareX
Keyviz
Brave

## Audio Setup

Install [FxSound](https://www.fxsound.com/) and set as default device
Disable all FxSound keybindings
Set speakers as default device in FxSound control panel
Set OBS audio monitoring to monitor (mute output)
Install Voicemeeter Banana
Setup one virtual input to accept all communications audio and make it the default communications device on Windows
Setup another virtual input to accept audio routed and filtered from OBS and make it the default input device on Windows

## Configurations

AHK scripts

```ahk title="Sleep.ahk"
#Requires AutoHotkey v2.0+
#SingleInstance Force

#^q:: ; Windows + Ctrl + Q
{
    Sleep 100  ; Small delay to prevent accidental key interference
    DllCall("PowrProf\SetSuspendState", "Int", 0, "Int", 1, "Int", 0)
}
```

```ahk title="OBS.ahk"
#Requires AutoHotkey v2.0+
#SingleInstance Force

obsPath := "C:\Program Files\obs-studio\bin\64bit\obs64.exe"

LaunchOBS()
{
    if ProcessExist("obs64.exe")
        return
    Run obsPath, "C:\Program Files\obs-studio\bin\64bit"
}

ExitOBS()
{
    if ProcessExist("obs64.exe") {
        Run "taskkill.exe /IM obs64.exe",,"Hide"
    }
}

Main()
{
    if ProcessExist("Discord.exe")
    {
        LaunchOBS
    }
    else if WinExist("ahk_exe ApplicationFrameHost.exe", "Unigram")
    {
        LaunchOBS
    }
    else if WinExist("ahk_exe ApplicationFrameHost.exe", "WhatsApp")
    {
        LaunchOBS
    }
    else
    {
        ExitOBS
    }
}

SetTimer(Main, 2000)
```

```cmd title="Lock Mic Volume.cmd"
nircmdc.exe loop 1 1000 setsysvolume 65536 default_record
```

Windows Terminal

```json
{
    "$help": "https://aka.ms/terminal-documentation",
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "actions": 
    [
        {
            "command": 
            {
                "action": "copy",
                "singleLine": false
            },
            "id": "User.copy.644BA8F2",
            "keys": "ctrl+c"
        },
        {
            "command": "paste",
            "id": "User.paste",
            "keys": "ctrl+v"
        },
        {
            "command": "find",
            "id": "User.find",
            "keys": "ctrl+shift+f"
        },
        {
            "command": 
            {
                "action": "splitPane",
                "split": "auto",
                "splitMode": "duplicate"
            },
            "id": "User.splitPane.A6751878",
            "keys": "alt+shift+d"
        }
    ],
    "centerOnLaunch": false,
    "copyFormatting": "none",
    "copyOnSelect": false,
    "defaultProfile": "{2c4de342-38b7-51cf-b940-2309a097f518}",
    "newTabMenu": 
    [
        {
            "type": "remainingProfiles"
        }
    ],
    "profiles": 
    {
        "defaults": 
        {
            "adjustIndistinguishableColors": "always",
            "antialiasingMode": "cleartype",
            "colorScheme": "Vesper",
            "cursorShape": "filledBox",
            "font": 
            {
                "face": "JetBrainsMono Nerd Font",
                "size": 11
            },
            "historySize": 32767,
            "intenseTextStyle": "all",
            "opacity": 75,
            "padding": "12",
            "useAcrylic": true
        },
        "list": 
        [
            {
                "commandline": "%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe -NoLogo",
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": false,
                "name": "Windows PowerShell"
            },
            {
                "commandline": "%SystemRoot%\\System32\\cmd.exe",
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": true,
                "name": "Command Prompt"
            },
            {
                "commandline": "C:\\WINDOWS\\system32\\wsl.exe -d Ubuntu -e /usr/bin/fish",
                "guid": "{2c4de342-38b7-51cf-b940-2309a097f518}",
                "hidden": false,
                "name": "Ubuntu",
                "source": "Windows.Terminal.Wsl",
                "startingDirectory": null
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": true,
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            },
            {
                "guid": "{2ece5bfe-50ed-5f3a-ab87-5cd4baafed2b}",
                "hidden": true,
                "name": "Git Bash",
                "source": "Git"
            },
            {
                "guid": "{51855cb2-8cce-5362-8f54-464b92b32386}",
                "hidden": true,
                "name": "Ubuntu",
                "source": "CanonicalGroupLimited.Ubuntu_79rhkp1fndgsc"
            }
        ]
    },
    "schemes": 
    [
        {
            "background": "#101010",
            "black": "#101010",
            "blue": "#ACA1CE",
            "brightBlack": "#282828",
            "brightBlue": "#B9AEDA",
            "brightCyan": "#A0A0A0",
            "brightGreen": "#99FFE4",
            "brightPurple": "#ECAAD6",
            "brightRed": "#FF8080",
            "brightWhite": "#FFFFFF",
            "brightYellow": "#FFC799",
            "cursorColor": "#AEAFAD",
            "cyan": "#FFFFFF",
            "foreground": "#FFFFFF",
            "green": "#8FB99F",
            "name": "Vesper",
            "purple": "#E29ECA",
            "red": "#F5A191",
            "selectionBackground": "#323232",
            "white": "#A0A0A0",
            "yellow": "#E6B99D"
        }
    ],
    "theme": "Vesper",
    "themes": 
    [
        {
            "name": "Vesper",
            "tab": 
            {
                "background": "#202020FF",
                "iconStyle": "default",
                "showCloseButton": "always",
                "unfocusedBackground": null
            },
            "tabRow": 
            {
                "background": "#101010FF",
                "unfocusedBackground": "#101010FF"
            },
            "window": 
            {
                "applicationTheme": "dark",
                "experimental.rainbowFrame": false,
                "frame": null,
                "unfocusedFrame": null,
                "useMica": false
            }
        }
    ],
    "useAcrylicInTabRow": true
}
```

FanControl

```json
{
  "__VERSION__": "212",
  "Main": {
    "Controls": [
      {
        "Calibration": [],
        "Enable": false,
        "ForceApply": false,
        "Identifier": "/lpc/nct6799d/control/0",
        "IsHidden": true,
        "ManualControl": false,
        "ManualControlValue": 50,
        "MinimumPercent": 0,
        "Name": "Fan #1",
        "NickName": "Fan #1",
        "PairedFanSensor": null,
        "SelectedCommandStepDown": 8.0,
        "SelectedCommandStepUp": 8.0,
        "SelectedFanCurve": null,
        "SelectedOffset": 0,
        "SelectedStart": 0,
        "SelectedStop": 0
      },
      {
        "Calibration": [
          [
            0,
            452
          ],
          [
            10,
            454
          ],
          [
            20,
            481
          ],
          [
            30,
            678
          ],
          [
            40,
            874
          ],
          [
            50,
            1041
          ],
          [
            60,
            1204
          ],
          [
            70,
            1354
          ],
          [
            80,
            1496
          ],
          [
            90,
            1617
          ],
          [
            100,
            1878
          ]
        ],
        "Enable": true,
        "ForceApply": false,
        "Identifier": "/lpc/nct6799d/control/1",
        "IsHidden": false,
        "ManualControl": false,
        "ManualControlValue": 50,
        "MinimumPercent": 0,
        "Name": "Fan #2",
        "NickName": "AIO CPU Radiator",
        "PairedFanSensor": {
          "Identifier": "/lpc/nct6799d/fan/1",
          "IsHidden": false,
          "Name": "Fan #2",
          "NickName": "AIO CPU Radiator"
        },
        "SelectedCommandStepDown": 8.0,
        "SelectedCommandStepUp": 8.0,
        "SelectedFanCurve": {
          "CommandMode": 0,
          "IgnoreHysteresisAtLimits": true,
          "IsHidden": false,
          "MaximumCommand": 100,
          "MaximumTemperature": 100.0,
          "MinimumTemperature": 20.0,
          "Name": "CPU Temp",
          "OneWayHysteresis": false,
          "Points": [
            "40,20",
            "46,70",
            "60,80",
            "70,90",
            "75,100"
          ],
          "SelectedHysteresis": 2.0,
          "SelectedResponseTime": 1,
          "SelectedTempSource": {
            "Identifier": "/amdcpu/0/temperature/2",
            "IsHidden": false,
            "Name": "Core (Tctl/Tdie)",
            "NickName": "Core (Tctl/Tdie)"
          }
        },
        "SelectedOffset": 0,
        "SelectedStart": 0,
        "SelectedStop": 0
      },
      {
        "Calibration": [],
        "Enable": false,
        "ForceApply": false,
        "Identifier": "/lpc/nct6799d/control/2",
        "IsHidden": true,
        "ManualControl": false,
        "ManualControlValue": 50,
        "MinimumPercent": 0,
        "Name": "Fan #3",
        "NickName": "Fan #3",
        "PairedFanSensor": null,
        "SelectedCommandStepDown": 8.0,
        "SelectedCommandStepUp": 8.0,
        "SelectedFanCurve": null,
        "SelectedOffset": 0,
        "SelectedStart": 0,
        "SelectedStop": 0
      },
      {
        "Calibration": [
          [
            30,
            0
          ],
          [
            40,
            1447
          ],
          [
            50,
            1753
          ],
          [
            60,
            2045
          ],
          [
            70,
            2300
          ],
          [
            80,
            2553
          ],
          [
            90,
            2774
          ],
          [
            100,
            2935
          ]
        ],
        "Enable": true,
        "ForceApply": false,
        "Identifier": "/lpc/nct6799d/control/3",
        "IsHidden": false,
        "ManualControl": false,
        "ManualControlValue": 50,
        "MinimumPercent": 0,
        "Name": "Fan #4",
        "NickName": "AIO CPU Pump",
        "PairedFanSensor": {
          "Identifier": "/lpc/nct6799d/fan/3",
          "IsHidden": false,
          "Name": "Fan #4",
          "NickName": "AIO CPU Pump"
        },
        "SelectedCommandStepDown": 8.0,
        "SelectedCommandStepUp": 8.0,
        "SelectedFanCurve": {
          "CommandMode": 0,
          "IsHidden": true,
          "Name": "AIO",
          "Percent": 100.0
        },
        "SelectedOffset": 0,
        "SelectedStart": 39,
        "SelectedStop": 36
      },
      {
        "Calibration": [
          [
            10,
            0
          ],
          [
            20,
            402
          ],
          [
            30,
            629
          ],
          [
            40,
            824
          ],
          [
            50,
            992
          ],
          [
            60,
            1150
          ],
          [
            70,
            1288
          ],
          [
            80,
            1420
          ],
          [
            90,
            1535
          ],
          [
            100,
            1630
          ]
        ],
        "Enable": true,
        "ForceApply": false,
        "Identifier": "/lpc/nct6799d/control/4",
        "IsHidden": false,
        "ManualControl": false,
        "ManualControlValue": 50,
        "MinimumPercent": 0,
        "Name": "Fan #5",
        "NickName": "Case Fans",
        "PairedFanSensor": {
          "Identifier": "/lpc/nct6799d/fan/4",
          "IsHidden": false,
          "Name": "Fan #5",
          "NickName": "Case Fans"
        },
        "SelectedCommandStepDown": 8.0,
        "SelectedCommandStepUp": 8.0,
        "SelectedFanCurve": {
          "CommandMode": 0,
          "IsHidden": false,
          "Name": "Airflow",
          "SelectedFanCurves": [
            {
              "CommandMode": 0,
              "IgnoreHysteresisAtLimits": true,
              "IsHidden": false,
              "MaximumCommand": 100,
              "MaximumTemperature": 100.0,
              "MinimumTemperature": 20.0,
              "Name": "CPU Temp",
              "OneWayHysteresis": false,
              "Points": [
                "40,20",
                "46,70",
                "60,80",
                "70,90",
                "75,100"
              ],
              "SelectedHysteresis": 2.0,
              "SelectedResponseTime": 1,
              "SelectedTempSource": {
                "Identifier": "/amdcpu/0/temperature/2",
                "IsHidden": false,
                "Name": "Core (Tctl/Tdie)",
                "NickName": "Core (Tctl/Tdie)"
              }
            },
            {
              "CommandMode": 0,
              "IgnoreHysteresisAtLimits": true,
              "IsHidden": false,
              "MaximumCommand": 100,
              "MaximumTemperature": 100.0,
              "MinimumTemperature": 20.0,
              "Name": "GPU Temp",
              "OneWayHysteresis": false,
              "Points": [
                "30,30",
                "80,80"
              ],
              "SelectedHysteresis": 2.0,
              "SelectedResponseTime": 1,
              "SelectedTempSource": {
                "Identifier": "NVApiWrapper/0-AD107-A/sensor/0",
                "IsHidden": false,
                "Name": "GPU",
                "NickName": "GPU"
              }
            },
            {
              "CommandMode": 0,
              "IgnoreHysteresisAtLimits": true,
              "IsHidden": false,
              "MaximumCommand": 100,
              "MaximumTemperature": 80.0,
              "MinimumTemperature": 20.0,
              "Name": "Internals",
              "OneWayHysteresis": false,
              "Points": [
                "40,20",
                "80,100"
              ],
              "SelectedHysteresis": 2.0,
              "SelectedResponseTime": 1,
              "SelectedTempSource": {
                "Identifier": "Mix/Components",
                "IsHidden": false,
                "Name": "Components",
                "SelectedMixFunction": 0,
                "SelectedSensors": [
                  {
                    "Identifier": "Mix/Motherboard",
                    "IsHidden": false,
                    "Name": "Motherboard",
                    "SelectedMixFunction": 1,
                    "SelectedSensors": [
                      {
                        "Identifier": "/lpc/nct6799d/temperature/1",
                        "IsHidden": false,
                        "Name": "Temperature #1",
                        "NickName": "Temperature #1"
                      },
                      {
                        "Identifier": "/lpc/nct6799d/temperature/2",
                        "IsHidden": false,
                        "Name": "Temperature #2",
                        "NickName": "Temperature #2"
                      },
                      {
                        "Identifier": "/lpc/nct6799d/temperature/3",
                        "IsHidden": false,
                        "Name": "Temperature #3",
                        "NickName": "Temperature #3"
                      },
                      {
                        "Identifier": "/lpc/nct6799d/temperature/4",
                        "IsHidden": false,
                        "Name": "Temperature #4",
                        "NickName": "Temperature #4"
                      },
                      {
                        "Identifier": "/lpc/nct6799d/temperature/5",
                        "IsHidden": false,
                        "Name": "Temperature #5",
                        "NickName": "Temperature #5"
                      },
                      {
                        "Identifier": "/lpc/nct6799d/temperature/6",
                        "IsHidden": false,
                        "Name": "Temperature #6",
                        "NickName": "Temperature #6"
                      }
                    ]
                  },
                  {
                    "Identifier": "/nvme/0/temperature/0",
                    "IsHidden": false,
                    "Name": "Temperature",
                    "NickName": "Temperature"
                  },
                  {
                    "Identifier": "/amdcpu/0/temperature/2",
                    "IsHidden": false,
                    "Name": "Core (Tctl/Tdie)",
                    "NickName": "Core (Tctl/Tdie)"
                  },
                  {
                    "Identifier": "/amdcpu/0/temperature/3",
                    "IsHidden": false,
                    "Name": "CCD1 (Tdie)",
                    "NickName": "CCD1 (Tdie)"
                  },
                  {
                    "Identifier": "NVApiWrapper/0-AD107-A/sensor/0",
                    "IsHidden": false,
                    "Name": "GPU",
                    "NickName": "GPU"
                  }
                ]
              }
            }
          ],
          "SelectedMixFunction": 2
        },
        "SelectedOffset": 0,
        "SelectedStart": 40,
        "SelectedStop": 16
      },
      {
        "Calibration": [],
        "Enable": false,
        "ForceApply": false,
        "Identifier": "/lpc/nct6799d/control/5",
        "IsHidden": true,
        "ManualControl": false,
        "ManualControlValue": 50,
        "MinimumPercent": 0,
        "Name": "Fan #6",
        "NickName": "Fan #6",
        "PairedFanSensor": null,
        "SelectedCommandStepDown": 8.0,
        "SelectedCommandStepUp": 8.0,
        "SelectedFanCurve": null,
        "SelectedOffset": 0,
        "SelectedStart": 0,
        "SelectedStop": 0
      },
      {
        "Calibration": [],
        "Enable": false,
        "ForceApply": false,
        "Identifier": "/lpc/nct6799d/control/6",
        "IsHidden": true,
        "ManualControl": false,
        "ManualControlValue": 50,
        "MinimumPercent": 0,
        "Name": "Fan #7",
        "NickName": "Fan #7",
        "PairedFanSensor": null,
        "SelectedCommandStepDown": 8.0,
        "SelectedCommandStepUp": 8.0,
        "SelectedFanCurve": null,
        "SelectedOffset": 0,
        "SelectedStart": 0,
        "SelectedStop": 0
      },
      {
        "Calibration": [
          [
            30,
            893
          ],
          [
            40,
            1228
          ],
          [
            50,
            1561
          ],
          [
            60,
            1889
          ],
          [
            70,
            2227
          ],
          [
            80,
            2566
          ],
          [
            90,
            2888
          ],
          [
            100,
            3156
          ]
        ],
        "Enable": true,
        "ForceApply": false,
        "Identifier": "NVApiWrapper/0-AD107-A/control/0",
        "IsHidden": false,
        "ManualControl": false,
        "ManualControlValue": 50,
        "MinimumPercent": 0,
        "Name": "Control 1 - NVIDIA GeForce RTX 4060",
        "NickName": "NVIDIA GeForce RTX 4060",
        "PairedFanSensor": {
          "Identifier": "NVApiWrapper/0-AD107-A/fan/0",
          "IsHidden": false,
          "Name": "Fan 1 - NVIDIA GeForce RTX 4060",
          "NickName": "NVIDIA GeForce RTX 4060"
        },
        "SelectedCommandStepDown": 8.0,
        "SelectedCommandStepUp": 8.0,
        "SelectedFanCurve": {
          "CommandMode": 0,
          "IgnoreHysteresisAtLimits": true,
          "IsHidden": false,
          "MaximumCommand": 100,
          "MaximumTemperature": 100.0,
          "MinimumTemperature": 20.0,
          "Name": "GPU Temp",
          "OneWayHysteresis": false,
          "Points": [
            "30,30",
            "80,80"
          ],
          "SelectedHysteresis": 2.0,
          "SelectedResponseTime": 1,
          "SelectedTempSource": {
            "Identifier": "NVApiWrapper/0-AD107-A/sensor/0",
            "IsHidden": false,
            "Name": "GPU",
            "NickName": "GPU"
          }
        },
        "SelectedOffset": 0,
        "SelectedStart": 0,
        "SelectedStop": 0
      }
    ],
    "CustomSensors": [
      {
        "Identifier": "Mix/Motherboard",
        "IsHidden": false,
        "Name": "Motherboard",
        "SelectedMixFunction": 1,
        "SelectedSensors": [
          {
            "Identifier": "/lpc/nct6799d/temperature/1",
            "IsHidden": false,
            "Name": "Temperature #1",
            "NickName": "Temperature #1"
          },
          {
            "Identifier": "/lpc/nct6799d/temperature/2",
            "IsHidden": false,
            "Name": "Temperature #2",
            "NickName": "Temperature #2"
          },
          {
            "Identifier": "/lpc/nct6799d/temperature/3",
            "IsHidden": false,
            "Name": "Temperature #3",
            "NickName": "Temperature #3"
          },
          {
            "Identifier": "/lpc/nct6799d/temperature/4",
            "IsHidden": false,
            "Name": "Temperature #4",
            "NickName": "Temperature #4"
          },
          {
            "Identifier": "/lpc/nct6799d/temperature/5",
            "IsHidden": false,
            "Name": "Temperature #5",
            "NickName": "Temperature #5"
          },
          {
            "Identifier": "/lpc/nct6799d/temperature/6",
            "IsHidden": false,
            "Name": "Temperature #6",
            "NickName": "Temperature #6"
          }
        ]
      },
      {
        "Identifier": "Mix/Components",
        "IsHidden": false,
        "Name": "Components",
        "SelectedMixFunction": 0,
        "SelectedSensors": [
          {
            "Identifier": "Mix/Motherboard",
            "IsHidden": false,
            "Name": "Motherboard",
            "SelectedMixFunction": 1,
            "SelectedSensors": [
              {
                "Identifier": "/lpc/nct6799d/temperature/1",
                "IsHidden": false,
                "Name": "Temperature #1",
                "NickName": "Temperature #1"
              },
              {
                "Identifier": "/lpc/nct6799d/temperature/2",
                "IsHidden": false,
                "Name": "Temperature #2",
                "NickName": "Temperature #2"
              },
              {
                "Identifier": "/lpc/nct6799d/temperature/3",
                "IsHidden": false,
                "Name": "Temperature #3",
                "NickName": "Temperature #3"
              },
              {
                "Identifier": "/lpc/nct6799d/temperature/4",
                "IsHidden": false,
                "Name": "Temperature #4",
                "NickName": "Temperature #4"
              },
              {
                "Identifier": "/lpc/nct6799d/temperature/5",
                "IsHidden": false,
                "Name": "Temperature #5",
                "NickName": "Temperature #5"
              },
              {
                "Identifier": "/lpc/nct6799d/temperature/6",
                "IsHidden": false,
                "Name": "Temperature #6",
                "NickName": "Temperature #6"
              }
            ]
          },
          {
            "Identifier": "/nvme/0/temperature/0",
            "IsHidden": false,
            "Name": "Temperature",
            "NickName": "Temperature"
          },
          {
            "Identifier": "/amdcpu/0/temperature/2",
            "IsHidden": false,
            "Name": "Core (Tctl/Tdie)",
            "NickName": "Core (Tctl/Tdie)"
          },
          {
            "Identifier": "/amdcpu/0/temperature/3",
            "IsHidden": false,
            "Name": "CCD1 (Tdie)",
            "NickName": "CCD1 (Tdie)"
          },
          {
            "Identifier": "NVApiWrapper/0-AD107-A/sensor/0",
            "IsHidden": false,
            "Name": "GPU",
            "NickName": "GPU"
          }
        ]
      }
    ],
    "Fahrenheit": false,
    "FanCurves": [
      {
        "CommandMode": 0,
        "IgnoreHysteresisAtLimits": true,
        "IsHidden": false,
        "MaximumCommand": 100,
        "MaximumTemperature": 100.0,
        "MinimumTemperature": 20.0,
        "Name": "CPU Temp",
        "OneWayHysteresis": false,
        "Points": [
          "40,20",
          "46,70",
          "60,80",
          "70,90",
          "75,100"
        ],
        "SelectedHysteresis": 2.0,
        "SelectedResponseTime": 1,
        "SelectedTempSource": {
          "Identifier": "/amdcpu/0/temperature/2",
          "IsHidden": false,
          "Name": "Core (Tctl/Tdie)",
          "NickName": "Core (Tctl/Tdie)"
        }
      },
      {
        "CommandMode": 0,
        "IgnoreHysteresisAtLimits": true,
        "IsHidden": false,
        "MaximumCommand": 100,
        "MaximumTemperature": 100.0,
        "MinimumTemperature": 20.0,
        "Name": "GPU Temp",
        "OneWayHysteresis": false,
        "Points": [
          "30,30",
          "80,80"
        ],
        "SelectedHysteresis": 2.0,
        "SelectedResponseTime": 1,
        "SelectedTempSource": {
          "Identifier": "NVApiWrapper/0-AD107-A/sensor/0",
          "IsHidden": false,
          "Name": "GPU",
          "NickName": "GPU"
        }
      },
      {
        "CommandMode": 0,
        "IgnoreHysteresisAtLimits": true,
        "IsHidden": false,
        "MaximumCommand": 100,
        "MaximumTemperature": 80.0,
        "MinimumTemperature": 20.0,
        "Name": "Internals",
        "OneWayHysteresis": false,
        "Points": [
          "40,20",
          "80,100"
        ],
        "SelectedHysteresis": 2.0,
        "SelectedResponseTime": 1,
        "SelectedTempSource": {
          "Identifier": "Mix/Components",
          "IsHidden": false,
          "Name": "Components",
          "SelectedMixFunction": 0,
          "SelectedSensors": [
            {
              "Identifier": "Mix/Motherboard",
              "IsHidden": false,
              "Name": "Motherboard",
              "SelectedMixFunction": 1,
              "SelectedSensors": [
                {
                  "Identifier": "/lpc/nct6799d/temperature/1",
                  "IsHidden": false,
                  "Name": "Temperature #1",
                  "NickName": "Temperature #1"
                },
                {
                  "Identifier": "/lpc/nct6799d/temperature/2",
                  "IsHidden": false,
                  "Name": "Temperature #2",
                  "NickName": "Temperature #2"
                },
                {
                  "Identifier": "/lpc/nct6799d/temperature/3",
                  "IsHidden": false,
                  "Name": "Temperature #3",
                  "NickName": "Temperature #3"
                },
                {
                  "Identifier": "/lpc/nct6799d/temperature/4",
                  "IsHidden": false,
                  "Name": "Temperature #4",
                  "NickName": "Temperature #4"
                },
                {
                  "Identifier": "/lpc/nct6799d/temperature/5",
                  "IsHidden": false,
                  "Name": "Temperature #5",
                  "NickName": "Temperature #5"
                },
                {
                  "Identifier": "/lpc/nct6799d/temperature/6",
                  "IsHidden": false,
                  "Name": "Temperature #6",
                  "NickName": "Temperature #6"
                }
              ]
            },
            {
              "Identifier": "/nvme/0/temperature/0",
              "IsHidden": false,
              "Name": "Temperature",
              "NickName": "Temperature"
            },
            {
              "Identifier": "/amdcpu/0/temperature/2",
              "IsHidden": false,
              "Name": "Core (Tctl/Tdie)",
              "NickName": "Core (Tctl/Tdie)"
            },
            {
              "Identifier": "/amdcpu/0/temperature/3",
              "IsHidden": false,
              "Name": "CCD1 (Tdie)",
              "NickName": "CCD1 (Tdie)"
            },
            {
              "Identifier": "NVApiWrapper/0-AD107-A/sensor/0",
              "IsHidden": false,
              "Name": "GPU",
              "NickName": "GPU"
            }
          ]
        }
      },
      {
        "CommandMode": 0,
        "IsHidden": true,
        "Name": "AIO",
        "Percent": 100.0
      },
      {
        "CommandMode": 0,
        "IsHidden": false,
        "Name": "Airflow",
        "SelectedFanCurves": [
          {
            "CommandMode": 0,
            "IgnoreHysteresisAtLimits": true,
            "IsHidden": false,
            "MaximumCommand": 100,
            "MaximumTemperature": 100.0,
            "MinimumTemperature": 20.0,
            "Name": "CPU Temp",
            "OneWayHysteresis": false,
            "Points": [
              "40,20",
              "46,70",
              "60,80",
              "70,90",
              "75,100"
            ],
            "SelectedHysteresis": 2.0,
            "SelectedResponseTime": 1,
            "SelectedTempSource": {
              "Identifier": "/amdcpu/0/temperature/2",
              "IsHidden": false,
              "Name": "Core (Tctl/Tdie)",
              "NickName": "Core (Tctl/Tdie)"
            }
          },
          {
            "CommandMode": 0,
            "IgnoreHysteresisAtLimits": true,
            "IsHidden": false,
            "MaximumCommand": 100,
            "MaximumTemperature": 100.0,
            "MinimumTemperature": 20.0,
            "Name": "GPU Temp",
            "OneWayHysteresis": false,
            "Points": [
              "30,30",
              "80,80"
            ],
            "SelectedHysteresis": 2.0,
            "SelectedResponseTime": 1,
            "SelectedTempSource": {
              "Identifier": "NVApiWrapper/0-AD107-A/sensor/0",
              "IsHidden": false,
              "Name": "GPU",
              "NickName": "GPU"
            }
          },
          {
            "CommandMode": 0,
            "IgnoreHysteresisAtLimits": true,
            "IsHidden": false,
            "MaximumCommand": 100,
            "MaximumTemperature": 80.0,
            "MinimumTemperature": 20.0,
            "Name": "Internals",
            "OneWayHysteresis": false,
            "Points": [
              "40,20",
              "80,100"
            ],
            "SelectedHysteresis": 2.0,
            "SelectedResponseTime": 1,
            "SelectedTempSource": {
              "Identifier": "Mix/Components",
              "IsHidden": false,
              "Name": "Components",
              "SelectedMixFunction": 0,
              "SelectedSensors": [
                {
                  "Identifier": "Mix/Motherboard",
                  "IsHidden": false,
                  "Name": "Motherboard",
                  "SelectedMixFunction": 1,
                  "SelectedSensors": [
                    {
                      "Identifier": "/lpc/nct6799d/temperature/1",
                      "IsHidden": false,
                      "Name": "Temperature #1",
                      "NickName": "Temperature #1"
                    },
                    {
                      "Identifier": "/lpc/nct6799d/temperature/2",
                      "IsHidden": false,
                      "Name": "Temperature #2",
                      "NickName": "Temperature #2"
                    },
                    {
                      "Identifier": "/lpc/nct6799d/temperature/3",
                      "IsHidden": false,
                      "Name": "Temperature #3",
                      "NickName": "Temperature #3"
                    },
                    {
                      "Identifier": "/lpc/nct6799d/temperature/4",
                      "IsHidden": false,
                      "Name": "Temperature #4",
                      "NickName": "Temperature #4"
                    },
                    {
                      "Identifier": "/lpc/nct6799d/temperature/5",
                      "IsHidden": false,
                      "Name": "Temperature #5",
                      "NickName": "Temperature #5"
                    },
                    {
                      "Identifier": "/lpc/nct6799d/temperature/6",
                      "IsHidden": false,
                      "Name": "Temperature #6",
                      "NickName": "Temperature #6"
                    }
                  ]
                },
                {
                  "Identifier": "/nvme/0/temperature/0",
                  "IsHidden": false,
                  "Name": "Temperature",
                  "NickName": "Temperature"
                },
                {
                  "Identifier": "/amdcpu/0/temperature/2",
                  "IsHidden": false,
                  "Name": "Core (Tctl/Tdie)",
                  "NickName": "Core (Tctl/Tdie)"
                },
                {
                  "Identifier": "/amdcpu/0/temperature/3",
                  "IsHidden": false,
                  "Name": "CCD1 (Tdie)",
                  "NickName": "CCD1 (Tdie)"
                },
                {
                  "Identifier": "NVApiWrapper/0-AD107-A/sensor/0",
                  "IsHidden": false,
                  "Name": "GPU",
                  "NickName": "GPU"
                }
              ]
            }
          }
        ],
        "SelectedMixFunction": 2
      }
    ],
    "FanSensors": [
      {
        "Identifier": "/lpc/nct6799d/fan/0",
        "IsHidden": false,
        "Name": "Fan #1",
        "NickName": "Fan #1"
      },
      {
        "Identifier": "/lpc/nct6799d/fan/1",
        "IsHidden": false,
        "Name": "Fan #2",
        "NickName": "AIO CPU Radiator"
      },
      {
        "Identifier": "/lpc/nct6799d/fan/2",
        "IsHidden": false,
        "Name": "Fan #3",
        "NickName": "Fan #3"
      },
      {
        "Identifier": "/lpc/nct6799d/fan/3",
        "IsHidden": false,
        "Name": "Fan #4",
        "NickName": "AIO CPU Pump"
      },
      {
        "Identifier": "/lpc/nct6799d/fan/4",
        "IsHidden": false,
        "Name": "Fan #5",
        "NickName": "Case Fans"
      },
      {
        "Identifier": "/lpc/nct6799d/fan/5",
        "IsHidden": false,
        "Name": "Fan #6",
        "NickName": "Fan #6"
      },
      {
        "Identifier": "/lpc/nct6799d/fan/6",
        "IsHidden": false,
        "Name": "Fan #7",
        "NickName": "Fan #7"
      },
      {
        "Identifier": "NVApiWrapper/0-AD107-A/fan/0",
        "IsHidden": false,
        "Name": "Fan 1 - NVIDIA GeForce RTX 4060",
        "NickName": "NVIDIA GeForce RTX 4060"
      }
    ],
    "HideCalibration": false,
    "HideFanSpeedCards": true,
    "HorizontalUIOrientation": false,
    "PrimaryColor": "#FF607D8B",
    "SecondaryColor": "#FFC6FF00",
    "SelectedTheme": "",
    "ShowHiddenCards": false,
    "SyncThemeWithWindows": true,
    "SyncTrayIconColorWithWindows": true,
    "TemperatureSensors": [],
    "TrayIconColor": null,
    "TrayIcons": []
  },
  "Sensors": {
    "AdlxWrapperSettings": {
      "Enabled": true
    },
    "DisabledPlugins": [],
    "DisableStorageSensors": false,
    "LibreHardwareMonitorSettings": {
      "Controller": true,
      "CPU": true,
      "EmbeddedEC": true,
      "GPU": true,
      "InpOut": false,
      "Memory": true,
      "Motherboard": true,
      "PSU": false,
      "Storage": true,
      "ZeroRPMOverride": false
    },
    "NvAPIWrapperSettings": {
      "Enabled": true,
      "ZeroRPMOverride": false
    },
    "SensorCount": 27
  }
}
```

Disable Windows built-in hotkeys

```reg
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced]
"DisabledHotkeys"="R"

;[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer]
;"NoWinKeys"=dword:00000001
```

### RGB LIGHTS

Script for me to use if I wish to configure my RGB lights on startup

(Without the program running all the time/autostarting on startup)

```cmd title="rgb.bat"
:: Wait for 2 minutes before closing
SET timeout=2

CD /d "C:\Program Files (x86)\ASRock Utility\ASRRGBLED\Bin"
START "ASRRGBLED" "C:\Program Files (x86)\ASRock Utility\ASRRGBLED\Bin\AsrPolychromeRGB.exe"

SET /a wait_for = 60 * timeout
TIMEOUT /t %wait_for% /nobreak
TASKKILL /IM "AsrPolychromeRGB.exe"
```
