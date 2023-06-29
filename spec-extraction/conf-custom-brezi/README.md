# Configuration files for Beli Brezi

Here we give a few of the configuration files used in the extraction of data during Beli Brezi 2022. To use, need to include as the config files in `spec-calibration.ipynb`.

## `catalogs`

Wavelength catalogues of the spectral lines of the calibration lamp. Our spectrograph uses an ArNe lamp, so the observations in the red part of the spectrum will use the Ne lines listed in the catalogues. See the package documentation for details on how to make your own catalogue.

## `instruments`

Basic information about the instruments and data files. The most important ones are the camera size and properties of the dispersion captured on the spectrum. The latter are approximate estimates of what is produced on the image; these provide an initial point for the calibration procedure to do its job. See the package documentation for details on how to make your own instrument configuration.

## `masks`

Mask description of the spectrograph. Provides information about where the spectral lines are. Required for the grism-type spectrographs which fold the whole spectrum in several stripes on the image. See the package documentation for details on how to make your own spectra masks.
