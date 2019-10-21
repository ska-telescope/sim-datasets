# Overview

This file describes a set of simulated visibility data and dirty images generated using a telescope model of SKA1-Low, and a sky model based on the GLEAM catalogue.

A summary of the data sets is available at:

- <https://confluence.skatelescope.org/display/SE/Simulated+data+set+specifications>

The data sets can be obtained from the Google Drive folder:

- <https://drive.google.com/open?id=1tq8jF0myYyk2BRgAaAyFlb4PcGzWXUtB>

(this includes sky model files, and sample dirty images produced using W-projection and 3D DFT)

The script used to generate the data sets and images can be found on GitLab at:

- <https://gitlab.com/ska-telescope/sim-datasets>

## Sky Model

The sky model is based on the GLEAM catalogue with sources extracted to cover the MWA EoR1 target field at (RA, Dec) = (60, -30) degrees.

## Telescope Model

The telescope model used station coordinates for SKA1-Low (from the document SKA-TEL-SKO-0000422 Revision 3), and a set of 512, 38-metre-diameter randomized station layouts, with each station containing 256 generic dipole antennas. The time- and frequency-dependent variation of each (different) station beam was modelled.

# Simulation & Imaging Script

Data were simulated and imaged using OSKAR (<https://github.com/OxfordSKA/OSKAR>). Dirty images were generated using both a 3D Direct Fourier Transform and also W-projection to allow for the investigation of errors introduced by the imaging process. The script uses the OSKAR Python bindings (<https://github.com/OxfordSKA/OSKAR/tree/master/python>).

# Data Set Summary

The requirements were outlined on the ticket SP-474, and consisted of three differently-sized data sets:

- Small: 10s of sources in a 2048 by 2048 image.
- Medium: 100s of sources in an 8192 by 8192 image.
- Large: 500+ sources in a 16384 by 16384 image.

We chose the field of view of the three images to cover (respectively) 1, 4 and 8 degrees, so the image resolution was kept constant. For the MWA EoR1 field, the corresponding source counts were:

- Small: 33 sources (within 0.707 degrees radius)
- Medium: 479 sources (within 2.828 degrees radius)
- Large: 1895 sources (within 5.657 degrees radius)

## Observation Parameters

- SKA1-Low has 130816 instantaneous baselines, and the large data set required ~30 million visibility samples in total. We chose the large data set to span 4 hours of observation time, and the medium and small data sets to span shorter observations at higher time resolution.
- We simulated a time average per data dump of 1 second.
- We simulated frequency channels 100 kHz-wide, starting at 140 MHz, and separated every 1 MHz.
- We used symmetric hour angle ranges in all cases.
- Only Stokes-I visibilities were generated.

## Large

Visibilities for the large data set were generated at 60 time samples over 4 hours (therefore with an interval of 4 minutes) and 4 frequency channels, to give 240 sets of baselines in total and thus 31,395,840 visibility samples.

## Medium

Visibilities for the medium data set were generated at 30 time samples over 1 hour (therefore with an interval of 2 minutes) and 2 frequency channels, to give 60 sets of baselines in total and thus 7,848,960 visibility samples.

## Small

Visibilities for the small data set were generated at 30 time samples over 15 minutes (therefore with an interval of 30 seconds) and 1 frequency channel, to give 30 sets of baselines and thus 3,924,480 visibility samples.

# Data Products

All computations used double-precision floating point arithmetic. Filenames in this section refer to the files in the Google Drive folder.

## Visibility Data

Visibilities were saved as Measurement Sets, and these were then compressed using ZIP. The Google Drive folder contains the three ZIP files:

- `sim_large.ms.zip`
- `sim_medium.ms.zip`
- `sim_small.ms.zip`

## Images

Images were saved as FITS files. Dirty images generated using W-projection have filenames prefixed with `img_wproj_` and those generated using 3D DFT are prefixed with `img_dft_`.

## Sky Models

Sky models, consisting of a list of point sources used to generate the three data sets, are provided in the text files:

- `sky_large.txt`
- `sky_medium.txt`
- `sky_small.txt`

## Telescope Model

The OSKAR telescope model folder used for the simulations is available inside the ZIP archive:

- `SKA1-LOW_SKO-0000422_Rev3_38m.tm.zip`
