Telluric-Fitter
===============

This code will fit the telluric absorption spectrum in data, using LBLRTM. More details can be found in the manual and examples, but the installation and run procedure are outlined below.


Installation
------------

To install this code, you will need to download lblrtm from http://rtweb.aer.com/lblrtm.html. Extract the package, and put the individual tar.gz files in the top-level directory. Alternatively, you can download the full TelFit source, which includes LBLRTM, from http://my.url.utexas.edu. Then, the command 

'''bash
python setup.py install
'''

should build lblrtm, and set up TelFit to run. It may take a while, as it is building inputs for the LBLRTM code.


Running TelFit
--------------

To run TelFit, you should create a script like in the examples. The key parts of the script are the inputs to the TelluricFitter class. You should:

  - Initialize fitter: fitter = TelluricFitter()
  - Define variables to fit: must provide a dictionary where
      the key is the name of the variable, and the value is
      the initial guess value for that variable.
      Example: fitter.FitVariable({"ch4": 1.6, "h2o": 45.0})
  - Edit values of constant parameters: similar to FitVariable,
      but the variables given here will not be fit. Useful for 
      settings things like the telescope pointing angle, temperature,
      and pressure, which will be very well-known.
      Example: fitter.AdjustValue({"angle": 50.6})
  - Set bounds on fitted variables (fitter.SetBounds): Give a dictionary
      where the key is the name of the variable, and the value is
      a list of size 2 of the form [lower_bound, upper_bound]
  - Import data (fitter.ImportData): Copy data as a class variable.
      Must be given as a DataStructures.xypoint instance
  - Perform the fit: (fitter.Fit):
      Returns a DataStructures.xypoint instance of the model. The 
      x-values in the returned array are the same as the data.
