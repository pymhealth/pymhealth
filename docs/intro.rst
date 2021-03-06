============
Introduction
============

Pymhealth is a python package for processing and extracting features from
mHealth sensors and data streams, particularly those from smartphones
and common wearable devices. It uses numba to compile functions where
it will provide a significant improvement over popular python data analysis
and signal processing packages, but will otherwise use and integrate itself
with the standard python data science stack.

------------
Installation
------------
Pymhealth is not yet provided on PyPI, it can be installed through
pip:
::
    $ pip install git+git://github.com/callumstew/pymhealth.git

You can also download or clone the repository and either install the
directory with pip or add the directory to your python path.

-----------------
Package structure
-----------------
There are two main subpackages: processing and features, for processing and
extracting features from mHealth data respectively. Each contains submodules
corresponding to common mHealth data streams (accelerometer, eda, telephony,
etc). There are also device specific preprocessing functions for some mHealth devicesand data (Fitbit, Empatica E4, Biovotion VSM1).
