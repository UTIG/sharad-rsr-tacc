# sharad-rsr-tacc

code for running RSR processing of SHARAD on TACC 
(using [SDS1-SHARAD](https://github.austin.utexas.edu/utig-reason/SDS1-SHARAD))


This code is meant to be run on a TACC login node, and it orchestrates
the synchronization of input data from the source storage servers (at UTIG) to
local storage at TACC, dispatching job requests to the TACC job scheduler,
and finally the synchronization of relevant output data at TACC back
to the source storage servers (at UTIG).


# Cloning

This repository uses [SDS1-SHARAD](https://github.austin.utexas.edu/utig-reason/SDS1-SHARAD)
 as a submodule, so you must use the --recursive option
when cloning.

```
git clone --recursive https://github.austin.utexas.edu/utig-reason/sharad-rsr-tacc.git
```


Submodules:
https://github.austin.utexas.edu/utig-reason/SDS1-SHARAD.git

Dependencies:

sharad-rsr-tacc and SHARAD1-SDS were both written for Python 3.9

# Initial release

These directions are for porting this code from UTIG's environment to TACC's.
Porting directions will be different for other target systems.
The example scripts in the env directory will need significant path changes.
Later releases will improve portability.


# Initial Configuration

- Get SPICE kernels
    * see env/get-kernels

      Note, these kernels come from JPL and must be stored on the specified path for them to be found.
      https://naif.jpl.nasa.gov/pub/naif/MRO/kernels/spk/

- Get PDS3 labels
    * see env/get-labels

      Like kernels, these labels come from the PDS node and must be stored in the correct location.
	https://pds-geosciences.wustl.edu/missions/mro/sharad.htm

- Get some data
    * see env/get-one, env/get-two, env/get-mrosh1

      Data initially came from the PDS node and is storied in the same arangement.  The first two examples are for single orbits.  The third grabs all of mrosh1.
	https://pds-geosciences.wustl.edu/missions/mro/sharad.htm

- Set up required python dependancies
    * Install them with pip

      Do a "pip3 install `cat SDS1-SHARAD/requirements.txt`"
    * Deal with failures

      At TACC multiple depenancies failed to install or function.  Directions for installing those can be found in env/get-gdal, env/get-h5py, and env/get-tables

- Rename path prefix
    * env/subs

	This converts the file structure prefix from UTIG's to TACC's.  Your system prefix will be different.
    * env/unsubs

        This can be used to convert the prefix back.  This is useful for doing git commits.


# Running

- Run jobs
    * pipeline.py

      The processing pipeline can be run by putting the full path to the data file ending in "_a_a.dat" into text file and passing that file as a tracklist.
	"./pipeline.py -vv --tracklist one.txt >& error"
    * env/run-back

      This is an example of how to run processing on the TACC Lonestar6 backent.

# Synchronize output data
    * env/put-all

      This is an example of how to copy processed data from TACC back to UTIG.
