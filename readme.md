# Project's goals

The goal of this project is to provide an easy-to-install set of python bindings around C++ implementations of image processing and computer vision algorithms from *Image Processing On Line* [IPOL](http://www.ipol.im/). 

IPOL is a great source of state-of-art algorithms in the domain of image processing and computer vision. For each accepted paper a demo is made available online which is very valuable as people can quickly test the algorithms without the need to install them on their own machines. However if one wants to reuse some of these algorithms as part of a larger project written in Python, there is still a non negligible cost associated with the process of downloading and compiling the code as well as writing the scripts that generate temporary input files, call the executable with the right arguments and load the results from the generated files. We aim at reducing that cost by proving a **pythonic interface to IPOL algorithms**.

The goal of the project **is not** to re-implement algorithm from IPOL in Python or Cython, but only to create interfaces with minimal modification of the original C++ code. 
The C++ code is not stored in this repository but downloaded during the installation and potential modifications on the C++ code are saved as patches. 
 
# Installation

using pip

	sudo pip install git+git://github.com/martinResearch/PyIPOL.git


local installation 

	wget https://github.com/martinResearch/PyIPOL/archive/master.zip --no-check-certificate
	unzip master.zip 
	cd PyIPOL-master
	python setup.py build_ext --inplace


# Available Bindings

we are using the same categorization as [IPOL](http://www.ipol.im/)

* 3D
 
* SEGMENTATION AND EDGES
	* A Review of Classic Edge Detectors [on IPOL](http://www.ipol.im/pub/art/2012/gjmr-lsd/)
	* LSD: a Line Segment Detector [on IPOL](http://www.ipol.im/pub/art/2015/35/)

# Related projects
* the IPOL in-browser demos can be downloaded an run locally using a local cherrypy based server and the code [here](https://githua matlb.com/carlodef/ipol_demo). Maybe that code could be used to help to write the python interfaces.
* Some Matlab interfaces to IPOL algorithms written by [Paul-Darius Sarmadi](http://sarmadi.fr/mex-ipol-library/) during a summer internship in 2014 are available [here](https://github.com/Paul-Darius/ipol-matlab). This project contains a report with guidelines to make IPOL code that can easily be interfaced with MATLAB.

# Limitations and possible improvements

* IPOL now *unfortunately* accepts Matlab code. Matlab code cannot easily be interfaced with python.
* When the code has been written with files as input/outputs it might be difficult to create an nice python interface without modifying the code. Maybe using memory-mapped files could be a solution to avoid writing files to disk. However a direct interface without memory copies should be preferred when possible. 
* As we do not store the C++ code in the repository, modifications in the compressed files on IPOL may break the bindings. We may need to store the IPOL codes in an other Git repository (or another branch?) to make things more robust.
* We could provide some PyQt widgets and some python tools provide an user experience that is closer to the online interactive demos, with buttons and sliders to set up the parameters.

# Examples 

Once installed examples can be found in 

	/usr/local/lib/python2.7/dist-packages/ipol/examples

If that is not the case you find where ipol has been installed from python using

	import ipol
	print ipol.path

you can launch an example directly from within python using a simple import, for example for lsd: 

	import ipol.examples.test_lsd

you can get the list of examples as follows :

	import ipol.examples
	print ipol.examples.list

or using 

	import ipol 
	import os
	print os.listdir(os.path.join(ipol.path,'examples'))

# Contributing

The easiest way might be to create interfaces through temporary files and reusing the online demos python codes available [here](http://dev.ipol.im/git/?p=colom/ipol_demo.git;a=summary). 

When the function has be written to take data arrays as input/output it should possible to provide them with data from numpy arrays without copies using the class *ArrayWrapper* defined in the file *_ipol.pyx*.

Detailed step-by-step explanation of how some bindings have been written will be added to the documentation.



