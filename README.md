## [Download latest release](https://github.com/lauralex/dwm_lut/releases/latest/download/Release.zip)


# About
This tool applies 3D LUTs to the Windows desktop by hooking into DWM. It works in both SDR and HDR modes, and uses tetrahedral interpolation on the LUT data. In SDR, blue-noise dithering is applied to the output to reduce banding.

Right now it should work on any 20H2 or 21H1 build of Windows 10, and also the current build of Windows 11, and I'll try to update it whenever a new version breaks it.

# Usage
Use DisplayCAL or similar to generate .cube LUT files of any size, run `DwmLutGUI.exe`, assign them to monitors and then click Apply. Note that LUTs cannot be applied to monitors that are in "Duplicate" mode.


For ColourSpace users with HT license level, 65^3 eeColor LUT .txt files are also supported.

HDR LUTs must use BT.2020 + SMPTE ST 2084 values as input and output.

Minimizing the GUI will make it disappear from the taskbar, and you can use the context menu of the tray icon to quickly apply or disable all LUTs. For automation, you can start the exe with any (sensible) combination of `-apply`,  `-disable`, `-minimize` and `-exit` as arguments.

Note: DirectFlip and MPO get force disabled on monitors with an active LUT. These features are designed to improve performance for some windowed applications by allowing them to bypass DWM (and therefore also the LUT). This ensures that LUTs get applied properly to all applications (except exclusive fullscreen ones).

# Compiling
Using MSYS2's mingw64 environment: Install `mingw-w64-x86_64-MinHook` and run
```
gcc dwm_lut.c -O3 -shared -static -s -lMinHook -ld3dcompiler -luuid -Wl,--exclude-all-symbols -o dwm_lut.dll
```

to generate the DLL.

As for the GUI, just open the project in Visual Studio and compile a x64 Release build.
