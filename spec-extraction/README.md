# Spectra Extraction

Routines to deal with spectra extraction.
(Under construction).

## About

These are routines to deal with spectra extraction. Equipment required to make such observation varies widely, so the routines here are specific to the equipment at Beli Brezi. We use the LHIRES III spectrograph (see [here](https://www.shelyak.com/produit/lhires-iii/?lang=en) for more) with an Ar-Ne wavelength calibration lamp and the science camera is SBIG ST-1603ME.

This setup is quite portable and the usual observational process includes mounting it every night and unmounting after observations conclude. Thus, the produced stellar spectra need to be extracted from the 2D images where the calibration process is repeated for each observational night. While this package is better suited for a stationary spectrograph setup (meaning the calibration models need to be updated occasionally), it provides improvement to the accuracy of results without increasing the work significantly compared with the IRAF procedures we used prior to this.

Included in this folder, we have:

* [Calibration of spectra](#calibration-of-spectra-spec-calibrationipynb)
* [2D to 1D extraction of stellar spectra](#2d-to-1d-extraction-of-stellar-spectra-spec-2d-to-1d-extractipynb)
* [2D to 1D extraction of extended object spectra](#2d-to-1d-extraction-of-planetary-spectra-extended-objects-spec-planet-extractipynb)

## Calibration of spectra: `spec-calibration.ipynb`

This routine uses the package [SpectraPy](https://mcfuman.gitlab.io/SpectraPy/) to calibrate the science image by wavelength using calibration images of a reference spectrum (note this package only works under Linux). This package provides a generic calibration procedure which is independent of the instrument used and can be suited to the user's particular needs.

Because of the generic nature of the procedure, the package assumes very little in terms of the experimental setup and tries to correct as many effects as possible. In our case, all of these are welcome improvements to the accuracy of results.

The input is the two type of images:

* science image, which needs to be wavelength calibrated,
* calibration image, which contains the reference spectra used for wavelength calibration.

Both of these images are 2D images and the calibration fitting produces a wavelength calibration for each pixel in the image. This is later used to extract the 1D spectra for science tasks.

The calibration is in a few steps, outlined in more detail in the package documentation. Before starting, we need to include some configuration files that give the specifications of the setup. A few example files can be found in the `conf-custom-brezi` folder.

The notebook closely follows the [calibration](https://mcfuman.gitlab.io/SpectraPy/models-calib.html), [model data tuning](https://mcfuman.gitlab.io/SpectraPy/data-calib.html), and [2D extraction](https://mcfuman.gitlab.io/SpectraPy/spectra-extraction.html) guides found in the package documentation, so the comments inside are rather sparse -- all information is given in the guides. There are quite a few places where some names or numerical values need to be changed given the specific job being done, so we recommend to carefully read through the whole notebook.

## 2D to 1D extraction of stellar spectra: `spec-2D-to-1D-extract.ipynb`

This routine extracts the 1D stellar spectra from the 2D image produced by the previous calibration step. It uses the pixel->wavelength calibration (represented by WCS system) by summing over the wavelength bins to 'fold' the axis of the image perpendicular to the dispersion axis.

This notebook was kindly provided by @mimirerelala.

## 2D to 1D extraction of planetary spectra (extended objects): `spec-planet-extract.ipynb`

Need to include from the project for Varna conf.
