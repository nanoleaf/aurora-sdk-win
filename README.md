# Installation Instructions

Cygwin is required to work with the SDK on Windows. For installation instructions, see [here](https://cygwin.com/install.html). During Cygwin install, make sure to select the following packages to be installed:

`make`

`gcc`

`g++`

`python`

`xinit`

`xorg-server`

In Cygwin, clone or download the appropriate SDK for Windows from our [GitHub Page](https://github.com/nanoleaf/aurora-sdk-win).

Navigate to the top-level SDK directory `aurora-sdk-win`.

Install numpy:

`pip install numpy`

Install remaining packages:

`pip install -r requirements.txt`

## Common Errors
### `python` and `pip` mismatch
If you have more than source of python and associated tools in Cygwin, please make sure `python` and `pip` belong to the same source (e.g., Cygwin native python 2, Cygwin native python 3, Anaconda, etc.).

To check, use `which -a python` and `which -a pip`, the first line displayed is the current source.

### Permissions
Check if the executables in the SDK have been granted execution privilege.

# Plugin Builder
The Plugin Builder tool is the preferred method for:

* Pairing with an Light Panels
* Using the Light Panels simulator
* Using plugin options
* Creating a palette
* Building and running plugins

In the directory plugin-builder-tool/ simply run the command: `python main.py`. A GUI will appear that prompts you to enter the IP address of the testing Light Panels (or use a simulator), your desired palette, and the absolute path to your plugin in the directory AuroraPluginTemplate/.

A GUI also exists to create Plugin Options for your plugin. The GUI reads and writes the given Plugin Options to the PluginOptions.h of whichever plugin is selected by the plugin location field.

To build and test a plugin, simply browse to the directory of the plugin, such as ``AuroraPluginTemplate``, pressing Build, then Upload & Run.

## Common Errors
If you encounter the following error message trying to run the Plugin Builder:

`_tkinter.TclError: no display name and no $DISPLAY environment variable`

Then xinit/xorg-server may not be running. In your Cygwin terminal, run the following command:

`export DISPLAY=:0.0`

If the same error still persists, run `XWin Server` from the Windows Start Menu, an application which should be installed with Cygwin.

## Working with Light Panels
If you have a set of Light Panels, you can view the plugin on the panels themselves from within Plugin Builder. The Light Panels must be connected to a WiFi network.

### IP Address
The IP address of your Light Panels can be determined by using [SSDP Scanner](https://www.microsoft.com/en-us/store/p/ssdp-scanner/9wzdncrcs2n7).

### Pairing
An initial pairing process is required to connect the Plugin Builder with Light Panels. This is a one-time process for each set of Light Panels.

Pairing Steps:
1. Enter the IP of the Light Panels and press Pair.
2. Hold down the power button on the Light Panels controller for 5-7 seconds
3. Press Enter in the Cygwin console

# Advanced Build and Test
If you do not wish to use the Plugin Builder GUI or run into errors while using it, you try to following advanced steps to build and test your plugin.

## Build
In Cygwin, navigate to the ``Debug`` folder inside a plugin directory such as ``AuroraPluginTemplate`` or ``Example\Converge``. Build using the following

`make clean`

`make`

If compilation completes successfully, a **libAuroraPlugin.so** file will be placed in the ``Debug`` folder.

## Test
The following requires up to 3 Cygwin consoles. All commands should be entered from the top-level SDK directory.

In console 1, enter

`python music_processor.py`

If you want to use the Light Panels simulator and your Python version is 2.7, in console 2, enter

`python LightPanelsSimulator/py27/light-panels-simulator.py`

If your Python version is 3.6, enter

`python LightPanelsSimulator/py3/light-panels-simulator.py`

No other python version is currently supported.

In console 3, enter

`./AnimationProcessor -p <absolute path to .so file> -i [<ip address>] [-s] [-cp <absolute path to palette file>] [-plugin_opts <absolute path to PluginOptions.h file]`

The *.so* file is the compiled plugin that you wish to run.

Enter the IP address of the Light Panels if you have them, otherwise, use ``-s`` to use Light Panels Simulator.

Use ``-cp`` to add the path to the palette file, if necessary.

Use ``-plugin_opt`` to add the path to the ``PluginOptions.h``, if necessary.
