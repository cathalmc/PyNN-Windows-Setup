# PyNN-Windows-Setup
How to get PyNN working in windows (2020)

As of 2020 getting pyNN (0.9.5) to work on Windows is a nightmare. From what I've gathered the issues is that one of the core files uses a forbidden name ("aux"), and as such if you try to install it with pip you will get an error like:

> The tar file X has a file (.../pyNN/hardware/aux.py) trying to install outside target directory (...\AppData\Local\Temp\pip-install\PyNN)

The work around for this is to install PyNN in developer mode:

## The fix:
* Download the zip file from: https://pypi.org/project/PyNN/#files
* Unzip the contents to a folder somewhere 
* Download and install anaconda if you do not already have it: https://www.anaconda.com/
* Create a conda environment just for PyNN 
* With the conda command line interface, use pip to install all the necessary dependencies as stated on http://neuralensemble.org/docs/PyNN/installation.html. 
* Make sure NEURON has been installed too (or whatever base simulator you wish to use)
* Use pip install -e /path/to/package/PyNN-0.9.5 to install the PyNN package in developer mode

Now PyNN will be installed in developer mode, but should otherwise work as expected. 

If using NEURON as the base simulator:
* Using the windows command line, navigate to ...\PyNN-0.9.5\pyNN\neuron\nmodl and run the "nrnivmodl" command to compile the mod files
* Open the PyNN-0.9.5\pyNN\neuron\simulator.py file with an editor and under the load_mechanisms(path) function, change the line: lib_path = os.path.join(path, arch, '.libs', 'libnrnmech.so') to lib_path = os.path.join(path, 'nrnmech.dll')


