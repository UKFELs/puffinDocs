# Links for Puffin

The Puffin source is managed and developed [from Github](https://github.com/UKFELs/Puffin). From there, we assign issues, and track various branches of development. It is recommended you fork to your own Github account and develop there, before submitting a pull request to the official UKFELs repo, so that it can be reviewed before integrating. For example, Lawrence Campbell's own forked version is [here](https://github.com/mightylorenzo/Puffin) - pull requests from here to the main repo upstream are submitted regularly.

When new commits are made, a Docker image to build and test Puffin is automatically built using Travis. Build results are shown [here](https://travis-ci.com/mightylorenzo/Puffin/branches). The status of the most recent builds of the master and dev branches are shown in badges on the UKFELs Puffin repo Readme. As time goes on, more unit tests should be added to ensure new builds are suitable for sending to users.

Docker images are stored [here](https://hub.docker.com/u/mightylorenzo/). These are currently **not** updated automatically for a successful Travis build. They must be built and updated manually.

Documentation is developed [here](https://github.com/UKFELs/puffinDocs) - which this record is a part of.

Puffin contains a collection of exemplar Python scripts to create input files, and analyse data. Please have a look around in the `utilities` directory, particularly the `pyPlotting` and `post` directories.

Paraffin is a Python package for beam matching, upsampling, and conversion to Puffin scaled units, of beams in the files stored in the SU format specified by the FXFEL project [here](https://github.com/UKFELs/FXFEL). Find Paraffin [here](https://github.com/UKFELs/Paraffin).

FXFELviz is a Python package for vizualizing and analyizing the SU format beams - see [here](https://github.com/mightylorenzo/FXFEL).
