# Beli Brezi FITS reduction scripts

Collection of scripts (notebooks) for reduction of FITS images and data extraction and manipulation.

## About the project

Under construction

## Table of Contents

* [About the project](#about-the-project)
* [Setup](#setup)
* [Implemented functionality](#implemented-functionality)
  * [Image preprocessing](#image-preprocessing-preprocessing)
  * [Spectra extraction](#spectra-extraction-spec-extraction)
  * [Spectra manipulation and visualisation](#spectra-manipulation-and-visualisation-spec-science)
* [Contributors](#contributors)
* [Licence](#licence)

## Setup

The processes in this repository use a number of `astropy` affiliated packages.

For inexperienced users, we recommend using Anaconda to manage python packages. The best practice is to set up a `conda` environment in Anaconda to separate the packages in use from other projects, under which you install all required packages. We provide a `.yml` file to facilitate the setup for some of these projects.

Note for the spectra extraction: the `spec-calibration.ipynb` uses the [SpectraPy](https://mcfuman.gitlab.io/SpectraPy/) package, which currently works only in Linux systems.

(TODO: so far the .yml is for the specific needs of the spectra group. Could extend to include packages for photometry, or provide .yml files for each of the categories implemented e.g. preproc, spectra extract etc.)

[//]: # (Need to expand more and explain why and how to do this in the terminal)

---

## Implemented functionality

Brief descriptions of the implemented functionality of the library. More details in the `README` files in each folder.

## Image Preprocessing: `preprocessing`

Deals with reducing images to prepare for scientific extraction. Currently only subtracts darks.

## Spectra Extraction: `spec-extraction`

Here, two steps are in line:

* Step 1: Calibrate the image by wavelength. This is done using the SpectraPy package, and requires a bit of tinkering and work by hand (by far the most tedious step).
* Step 2: Extract data. Here, depending on the type of object and science task, we have different approaches. In the case of stars, the extraction is done by the 2d-to-1d, and in the case of planets a basic extraction is done by the spec-edge-fit.

## Spectra manipulation and visualisation: `spec-science`

Various scripts that have been used in the last two years to handle 1d spectra and visualise results.

### `normalise-1d.ipynb`

Normalises along the continumm using `specutils`.

---

## Contributors

## Licence
