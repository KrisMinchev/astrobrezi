# Pipeline for data reduction using `ccdops`

This file contains the general description of the data pipeline that we will use for the initial ccd reduction to prepare data for analysis.

## Things to do:

Currently, it is a reduction pipeline focused on the way we prepare data for spectroscopic reduction. We should extend it to general reduction in the future by adding:

- biasing
- flat field reduction

Can extend this by, for example, adding flags at the start of the reduction notebook.

# Step One: Data Cleanup

This pipeline handles the whole data library using the `ccdproc` class `ImageFileCollection`. This allows us for quick filtering of images based on values in the header of each file. To be able to do this in the standardised way, we need to first make sure that all images conform to some simple criteria. We employ the Jupyter Notebook `data-cleanup.ipynb` for this task. This step can be skipped if the data already conforms to the requirements.

We need to make sure of two things:

- the header has a category named `'IMAGETYP'`, which specifies the type of image. We can choose between `['DARK', 'LIGHT', 'CALIB']` for the dark, science, and calibration lamp images respectively.
- the header has a category named `'BUNIT' = ADU`, which specifies the unit of signal in the images. This is needed so that images can be loaded as a `CCDData` type and the `ccdproc` functions can perform their operations.

You can find more information about how this is done [here](https://www.astropy.org/ccd-reduction-and-photometry-guide/v/dev/notebooks/01-11-reading-images.html).

