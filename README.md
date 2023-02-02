# sharad-rsr-tacc

code for running RSR processing of SHARAD on TACC 
(using [SDS1-SHARAD](https://github.austin.utexas.edu/utig-reason/SDS1-SHARAD))


This code is meant to be run on a TACC login node, and it orchestrates
the synchronization of input data from the source storage servers (at UTIG) to
local storage at TACC, dispatching job requests to the TACC job scheduler,
and finally the synchronization of relevant output data at TACC back
to the source storage servers (at UTIG).


# Cloning

This repository uses submodules, so you must use the --recursive option
when cloning.

Submodules:


Dependencies:

sharad-rsr-tacc and SHARAD1-SDS were both written for Python 3.9



# Initial Configuration

- Configure user options
  * Configure authentication keys
  * Where does user data come from at UTIG?
  * What data is sent back?

- Setup virtualenv

# Running

- Source environment rc file (setup environment variables and virtualenv)
- Synchronize input data
- Run jobs
- Synchronize output data
