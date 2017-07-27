# Installation Instructions

Clone or download the appropriate SDK repo for Windows from our [GitHub Page](https://github.com/nanoleaf/aurora-sdk-win)

In the SDK, the `music_processor` python script requires the latest version of the following (non-standard) python packages

* _numpy_
* _pyaudio_
* _librosa_

We highly recommend that you use a virtual environment to install these packages and to run the `music_processor` script. The following instructions will use `conda` to create virtual environments.

Cygwin is required to work with the SDK on Windows. For installation instructions, see [here](https://cygwin.com/install.html).

During Cygwin install, make sure to select the following packages:

`make`

`gcc`

`g++`

`python`

Install miniconda for Windows from [here](https://conda.io/miniconda.html). Make sure to select the option to **Add Anaconda to my PATH environment variable**.

The following should be executed within a Command Prompt.

Create and activate a virtual environment called `nanoleaf` (or any other name):

`conda create --name nanoleaf`

`activate nanoleaf`

Navigate to the top-level SDK directory `aurora-sdk-win`. It may be located within your Cygwin directory, for example, `C:\cygwin64\home\nanoleaf\aurora-sdk-win`.

Install numpy:

`conda install numpy`

Install pyaudio using `pip` (`conda install` will likely fail):

`pip install pyaudio`

Install librosa:

`conda install -c conda-forge librosa`

Install future (python 2.x users only):

`conda install future`

To deactivate the virtual environment:

`deactivate nanoleaf`

# Testing Your Plugin
## Compile Your Plugin
The _AuroraPlugin_ Framework comes with a makefile and a utilities library.
Once you have completed the implementation of your plugin, you can build it using the makefile in the Debug folder. If any additional libraries have been used, the makefile must be modified to link those libraries in as well during linking.

To compile, use a Cygwin terminal and change your working directory to the PluginSDK/Debug folder. Use the following commands:

`make clean`

`make`

Once the compilation completes successfully, a **libAuroraPlugin.so** file will be placed in the Debug folder which can be used with the simulator
## Run Your Plugin

Open up a Command Prompt and change your working directory to the PluginSDK folder. The `music_processor` python script must be run first with a virtual environment, enter:

`activate nanoleaf`

`python music_processor.py`

Open up a Cygwin terminal to run the sound module simulator, enter:

`./SoundModuleSimulator -p <absolute path to .so file> -i <ip address>`

If you generated a color palette (see Plugin Builder), enter:

`./SoundModuleSimulator -p <absolute path to .so file> -i <ip address> -cp <absolute path to palette file>`

The *.so* file is the compiled plugin that you wish to run on the Aurora. 

The IP address that you enter is the ip address of the Aurora on the local network. The ip address can be found by using [SSDP Scanner](https://www.microsoft.com/en-us/store/p/ssdp-scanner/9wzdncrcs2n7).

When using the simulator for the first time, the simulator will attempt to acquire an authentication token from the Aurora and ask the user to hold down the power button on the Aurora for 5-7 seconds. This step is not required during subsequent executions of the simulator. Note: the Simulator will only maintain authentication with one Aurora at a time.

## Plugin Builder
A plugin builder tool can be used to simplify the process of:

* _Pairing with an Aurora_
* _Creating a palette_

In the directory plugin-builder-tool/ simply run the command: `python main.py`. A GUI will appear that prompts you to enter the ip address of the testing Aurora, your desired palette, and the absolute path to your plugin in the directory AuroraPluginTemplate/.

Note that the Plugin Builder tool will output information to the terminal. Please check the terminal output for instructions, e.g., during pairing with Aurora or debug printouts from your plugin.
